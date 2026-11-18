# Agent guide: preparing wheel 3D models for the studio

Use this when you add, replace or wire a rim `.glb` for the FORGED 3D wheel studio.

The site code lives in `FazalRSA/Forgedwebsite`. This file describes that repo. The human version is `public/models/wheels/README.md` in that repo. Read it for background. Follow this file as the checklist.

## 1. Decide the wiring first

- **One model per design, not per listing.** `MODEL_URL_BY_CODE` in `src/data/catalogue.ts` maps `FSA002`, `FSA003`, `FSA004`, `FF-1` and `FF-3` to one shared file each. Every finish of a design reuses it. Check that map before you create a file.
- **Staggered sets use two files.** Front and rear are `modelUrl` and `rearModelUrl` on the listing. This adds a Front / Rear switch. FSA001 (`stf399-front.glb`, `stf399-rear.glb`) is the current case.
- **Listing records.** Set `"modelUrl": "/models/wheels/<file>.glb"` on the record in `src/data/customWheels.json`. Leading slash, no `public/`. Or use `npm run add-wheel -- --glb "/models/wheels/<file>.glb"`.
- **Cache.** `/models/*` is cached for one day (`render.yaml`). If a changed model must show at once, give it a new file name.

## 2. File format

- **Binary glTF 2.0, one `.glb`.** Buffers embedded. No external `.bin`. No textures: the shipped files have none.
- **Compression: meshopt and quantization.** The shipped files use `EXT_meshopt_compression` and `KHR_mesh_quantization`. The viewer decodes meshopt (`MeshoptDecoder` in `src/wheel-viewer/WheelStudio.tsx`).
- **Do not export Draco.** The viewer loads its decoder from `/draco/`, and this repo has no `public/draco/` folder. A Draco file would fail to load.
- **Clearcoat is allowed but not needed.** `KHR_materials_clearcoat` appears in every shipped file. The studio applies its own paint, and we have not verified any visible effect of clearcoat. Do not rely on it.
- **Budget.** Keep under about 150k triangles. Shipped files today: 60k to 99k triangles, and 0.37 to 0.81 MB each.

## 3. What goes in the file

- **Bare rim only.** No tyre, car, ground, lights or cameras.
- **Required sub-meshes, with these exact names:** `Rim_Barrel`, `Rim_Face_Spokes`, `Hardware_Bolts`, `Center_Cap`. A wheel with no cap may omit `Center_Cap`. FSA002 ships without one.
- **Optional brake meshes:** `Brake_Rotor` and `Brake_Caliper`. Their presence enables the brake clearance check.
- **Name nodes and meshes the same.** The shipped files do.

The studio classifies each mesh by name. The rules are in `classifyStudioPart` in `src/wheel-viewer/wheelStudioParts.ts`, applied in this order:

| Name contains | Part | Takes the finish |
|---|---|---|
| `caliper` | caliper (brake) | no |
| `rotor` or `disc` | rotor (brake) | no |
| `barrel` or `lip` | barrel | yes |
| `bolt`, `lug` or `hardware` | bolts | no, keeps its own material |
| `cap` | cap | yes |
| anything else | face | yes |

Avoid names that trip these rules by accident. `Flip` contains `lip`. `Capsule` contains `cap`. A face named `Disc_Spokes` becomes a brake rotor.

## 4. Orientation and units

- **Axle and face.** The studio finds the axle as the shortest direction of the rim and stands the wheel up. It then points the axle at the side where the cap (or face) sits, using names from section 3. Unnamed meshes face `+Z`. The viewer's `modelFlip` prop turns a model round, but no catalogue field sets it today, so fix a reversed file at source.
- **Authoring convention.** Export with the axle on `Z`, the front face toward `+Z` and up on `+Y`. Centre the file on the wheel. The studio re-centres on the bounding box anyway. The FSA and FF files follow this, with the axle on Z. The STF399 files have their axle on Y and load because the viewer turns them. Do not rely on that: new files follow the convention.
- **Real metres.** A 20 to 21 inch rim is about 0.50 to 0.55 m across. The studio shows a millimetre diameter only when the measured rim falls between 0.45 and 0.65 m. Outside that band the readout is hidden. Export in metres.
- **Bake transforms.** In Blender, apply scale and rotation (Ctrl+A) before export. The shipped files still carry node-level scale, which is legal glTF. A new export should not depend on it.

## 5. Materials

- **PBR metallic-roughness only.** No spec/gloss and no Phong.
- **No textures.** The studio paints each finish from `src/data/studioFinishes.ts` through `src/wheel-viewer/paint.ts`. Do not add BaseColor, Normal or ORM maps. The human README also has an older "2K textures" line that contradicts its own "no baked textures" rule. Follow the no-texture rule.

## 6. Export pipeline

1. **Source.** Model or scan the rim. Apply modifiers and transforms. Remove everything except the rim sub-meshes.
2. **Export from Blender.** File, Export, glTF 2.0. Format "glTF Binary (.glb)". Apply modifiers. Check "+Y Up".
3. **Compress.** Run glTF-Transform. Check the flags first, because the default changed between versions:

   ```bash
   npx @gltf-transform/cli optimize --help
   npx @gltf-transform/cli optimize in.glb out.glb --compress meshopt --texture-compress false
   npx @gltf-transform/cli inspect out.glb
   ```

4. **Place** the file in `public/models/wheels/`, then wire it as in section 1.

## 7. Checks before you open a pull request

- **Structure.** The four required sub-meshes are present. Their names pass the table in section 3. Triangles are under 150k and the file is about 1 MB or less.
- **Automated.** Run `npm install --legacy-peer-deps`, then `npm run lint`, `npm test` and `npm run build`. The catalogue tests fail if a listed wheel has no model file.
- **Visual, at 390 px width.** Open `/wheels/<slug>` (or `/studio/stf399` for the preview page). Confirm:
  - the model loads and the mesh counts appear;
  - finish swatches recolour the barrel, face and cap, while bolts keep their material;
  - the front view faces the viewer, and the spin is around the axle;
  - a broken file shows the retry card, and the console has no errors.
- **Viewer files.** Only edits under `src/wheel-viewer/` need the stamp (`npm run wheel-viewer:stamp`). A model file does not.

## 8. Accuracy and claims

- **Say how the model was made.** The FSA002, FSA003, FSA004, FF-1 and FF-3 models are traced from face-on photos, with simplified spokes and depth estimated. Only scans of the physical wheel count as scans.
- **Brake dimensions are assumed** for FSA001 (G80/G82 M3/M4 values). Do not present them as measured.
- **Do not invent specifications** in a pull request or on a page. Leave unknown values empty.

## 9. Do not

- Do not add Draco, textured or unbaked-transform models.
- Do not put models under `/models/rims/`. That path appears in the viewer README example. It does not exist.
- Do not edit `src/wheel-viewer/` to suit one model. It is shared with the BMW configurator. Edit it in this repo, stamp it, and tell the owner the configurator needs `node scripts/wheel-viewer-sync.mjs pull`.
- Do not push to `main`. Open a pull request. Every push to `main` deploys the live site.

## 10. Known drift to fix in the same pull request

- `public/models/wheels/README.md` says "one file per wheel finish" in its file specification. Its earlier section says one file per design. The code uses one per design.
- The same README gives a "2K BaseColor, Normal, ORM" texture spec. The same file says models ship without textures. Remove the texture line.
- `src/wheel-viewer/README.md` shows `/models/rims/forged_fsa002.glb`. The real folder is `/models/wheels/`.
- Clearcoat is in every shipped file and in no document.
