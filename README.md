# Awesome 3D Coding

Research on AI systems that write and execute programs to create, reconstruct, and edit 3D content. The program might be a Blender script that assembles a room, a CadQuery sketch that sets a hole diameter, or a Three.js scene that responds to user input.

<p align="center">
  <a href="#3d-coding-benchmarks">📏 Benchmarks</a> ·
  <a href="#datasets-for-3d-code">🗂️ Datasets</a> ·
  <a href="#models-for-3d-code-generation">🧩 Models</a> ·
  <a href="#3d-modeling-agents">🛠️ Agents</a> ·
  <a href="#evaluation-metrics">📐 Metrics</a>
</p>

## Table of Contents

- [3D Coding Benchmarks](#3d-coding-benchmarks)
  - [Asset Creation and Editing](#asset-creation-and-editing)
  - [CAD and Interactive Worlds](#cad-and-interactive-worlds)
- [Datasets for 3D Code](#datasets-for-3d-code)
  - [Procedural Assets and Scene Programs](#procedural-assets-and-scene-programs)
  - [Parametric CAD Programs](#parametric-cad-programs)
- [Models for 3D Code Generation](#models-for-3d-code-generation)
  - [Text to CAD](#text-to-cad)
  - [Shape to Code](#shape-to-code)
- [3D Modeling Agents](#3d-modeling-agents)
- [Evaluation Metrics](#evaluation-metrics)
- [Development Tools](#development-tools)
- [Related Collections](#related-collections)
- [Contributing](#contributing)

## 3D Coding Benchmarks

The output determines the test. A Blender asset can be compared with a reference from several viewpoints. A CAD part can be queried for dimensions and topology. An interactive world also needs tests that exercise its controls and inspect what changes.

### Asset Creation and Editing

| Benchmark | Year | Venue | Task and evaluation | Paper | Code | Project |
| --- | --- | --- | --- | --- | --- | --- |
| BlenderGym | 2025 | CVPR | Edit a starting Blender scene to match a target. Its 245 scenes cover geometry, lighting, materials, blend shapes, and placement. | [Paper](https://openaccess.thecvf.com/content/CVPR2025/html/Gu_BlenderGym_Benchmarking_Foundational_Model_Systems_for_Graphics_Editing_CVPR_2025_paper.html) | [Code](https://github.com/richard-guyunqi/BlenderGym-Open) | [Leaderboard](https://blendergym.github.io/) |
| 3DCodeBench | 2026 | NeurIPS | Write Blender Python from text or reference views across 212 asset categories. Scorers check execution, mesh geometry, and rendered appearance. | [Paper](https://arxiv.org/abs/2606.01057) | [Code](https://github.com/gaoypeng/3dcodebench) | [Leaderboard](https://www.3dcodebench.com/) |
| BlenderWorld | 2026 | arXiv | Deliver editable Blender projects for 223 creation briefs. Multi-view renders are scored against task-specific criteria and for overall visual quality. | [Paper](https://arxiv.org/abs/2610.23986) | [Code](https://github.com/QwenLM/BlenderWorld) | [Gallery](https://blenderworld.github.io/) |

### CAD and Interactive Worlds

| Benchmark | Year | Venue | Task and evaluation | Paper | Code | Project |
| --- | --- | --- | --- | --- | --- | --- |
| CADTestBench | 2026 | NeurIPS | Build a part from a written specification. Executable tests query the resulting solid for the geometric and topological properties requested in the prompt. | [Paper](https://arxiv.org/abs/2605.07807) | [Code](https://github.com/dimitrismallis/CADTestBench) | [Examples](https://dimitrismallis.github.io/cadtests/) |
| WorldCoder-Bench | 2026 | arXiv | Build an interactive Three.js world. StateProbe triggers actions in a browser and checks resulting state transitions. | [Paper](https://arxiv.org/abs/2606.01869) | [Code](https://github.com/shuolucs/WorldCoder-Bench) | — |

## Datasets for 3D Code

### Procedural Assets and Scene Programs

| Dataset | Reported scale | What a sample contains | Release |
| --- | --- | --- | --- |
| 3DCodeData | 12,720 asset instances from 212 procedural generators | One parameterized Blender asset with scripts, captions, four rendered views, and textured and geometry-only mesh exports. | [Dataset](https://huggingface.co/datasets/YipengGao/3DCode) |
| 3DCodeVerse-2M | 2,028,286 caption–program pairs in the merged text split | One caption paired with code. The same program can have several captions. The corpus spans Blender Python, CadQuery, OpenSCAD, Three.js, GLSL, and URDF. | [Dataset and schema](https://huggingface.co/datasets/3dcodeverse/3dcodeverse-2m) |

### Parametric CAD Programs

| Dataset | Reported scale | What a sample contains | Release |
| --- | --- | --- | --- |
| Text-to-CadQuery | 170,000 annotated Text2CAD examples | A part description paired with CadQuery code that constructs the solid. | [Annotations](https://huggingface.co/ricemonster/NeurIPS11092/blob/main/CadQuery.zip) · [Scripts](https://github.com/Text-to-CadQuery/Text-to-CadQuery) |
| CAD-Recode | 1 million generated CAD sequences in the ICCV study | A sequence of sketch and extrusion operations expressed in Python. The authors sample points on the resulting geometry to train a model to recover the code. | [Project and data releases](https://cad-recode.github.io/) |

## Models for 3D Code Generation

### Text to CAD

| Method | Year | Venue | Input → program | Highlight | Resources |
| --- | --- | --- | --- | --- | --- |
| Text-to-CadQuery | 2025 | arXiv | Part description → CadQuery Python | Fine-tunes language models to turn a specification into an editable parametric solid. | [Paper](https://arxiv.org/abs/2505.06507) · [Code](https://github.com/Text-to-CadQuery/Text-to-CadQuery) |
| CAD-Coder | 2025 | NeurIPS | Part description → CadQuery Python | Trains on paired examples, then uses distance between the generated and target shapes as a reward. | [Paper](https://arxiv.org/abs/2505.19713) · [Code](https://github.com/gudo7208/CAD-Coder) |

### Shape to Code

| Method | Year | Venue | Input → program | Highlight | Resources |
| --- | --- | --- | --- | --- | --- |
| CAD-Recode | 2025 | ICCV | Point cloud → CadQuery Python | Recovers the sketches and extrusions that build a solid. Editing a sketch dimension changes the reconstructed part. | [Paper](https://openaccess.thecvf.com/content/ICCV2025/html/Rukhovich_CAD-Recode_Reverse_Engineering_CAD_Code_from_Point_Clouds_ICCV_2025_paper.html) · [Code](https://github.com/filaPro/cad-recode) · [Project](https://cad-recode.github.io/) |
| MeshCoder | 2025 | NeurIPS | Point cloud → Blender Python | Represents a mesh as a program organized by part, so a user can modify one component of the reconstruction. | [Paper](https://arxiv.org/abs/2508.14879) · [Code](https://github.com/InternRobotics/MeshCoder) · [Project](https://daibingquan.github.io/MeshCoder/) |

## 3D Modeling Agents

| System | Year | Venue | Runtime | How the agent builds or revises a scene | Resources |
| --- | --- | --- | --- | --- | --- |
| SceneCraft | 2024 | ICML | Blender | Assembles assets from a scene description, checks their spatial relationships, and reuses placement functions across scenes. | [Paper](https://proceedings.mlr.press/v235/hu24g.html) |
| LL3M | 2025 | arXiv | Blender | Writes and debugs scripts for geometry and materials. Rendered views and follow-up instructions guide subsequent edits. | [Paper](https://arxiv.org/abs/2508.08228) · [Gallery](https://threedle.github.io/ll3m/) |
| 3DCodeVerse | 2026 | arXiv | Blender, CAD, and web graphics | Runs the generated program, measures the resulting asset, and inspects renders to identify which part of the program to revise. | [Paper](https://arxiv.org/abs/2610.22341) · [Code](https://github.com/gaoypeng/3dcodeverse) |

## Evaluation Metrics

| Property | Measure | What the evaluator inspects | Implementation or protocol |
| --- | --- | --- | --- |
| Executability | Execution rate | Whether each script completes in the target runtime. | [3DCodeBench scorers](https://github.com/gaoypeng/3dcodebench/blob/main/metrics/README.md) |
| Shape | Chamfer distance | Distances between points sampled on generated and reference surfaces. | [3DCodeBench scorers](https://github.com/gaoypeng/3dcodebench/blob/main/metrics/README.md) |
| Appearance | Multi-view image similarity | Corresponding renders of the generated and reference assets. Camera placement affects the comparison. | [3DCodeBench scorers](https://github.com/gaoypeng/3dcodebench/blob/main/metrics/README.md) |
| CAD requirements | Test pass rate | Predicates over a solid's geometry and topology, derived from the design brief. | [CADTests](https://github.com/dimitrismallis/CADTestBench) |
| Interactive behavior | Verification coverage | Runtime states and transitions observed while the evaluator interacts with the generated scene. | [StateProbe](https://arxiv.org/abs/2606.01869) |

## Development Tools

- **MCP for Blender** connects a coding agent to a running Blender session to inspect objects and execute Python edits. [Code](https://github.com/ahujasid/mcp-for-blender)
- **CQ-editor** provides a graphical debugger for CadQuery. Step through a generated script to see which operation changes a face, edge, or solid. [Code](https://github.com/CadQuery/CQ-editor)

## Related Collections

- **Awesome AIGC 3D** organizes 3D generation research by asset type and production stage. Its survey tables inspired the format of this collection. [Repository](https://github.com/hitcslj/Awesome-AIGC-3D)
- **Awesome Code as X** covers executable representations for agents. Its *Code as World* section includes scene and simulation programs. [Repository](https://github.com/kkakkkka/awesome-code-as-x)
- **Awesome 3D Skills** catalogs agent integrations for Blender, CAD systems, and game engines. [Repository](https://github.com/zhuyansen/awesome-3d-skills)

## Contributing

Add a row under the task your resource addresses and link to a primary source. For a method, identify the program it writes. For a benchmark, describe what gets checked after execution. For a dataset, give the counting unit and describe one sample.
