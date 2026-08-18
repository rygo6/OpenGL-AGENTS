---
name: opengl
description: Answer questions and help implement, debug, optimize, or test OpenGL and OpenGL ES by referencing local Khronos specifications, registries, reference pages, GLSL sources, conformance tests, tutorials, and Mesa source. Use for GL/GLES APIs, contexts, buffers, textures, framebuffers, shaders, pipelines, synchronization, extensions, platform bindings, driver behavior, and GL conformance. Always consult the local repos before answering.
---

# OpenGL Local Reference Skill

Always consult the relevant repositories in this skill's `references/` folder:

```text
references/OpenGL-Registry/   ← Khronos GL/GLES specs, headers, extensions, and XML registry
references/OpenGL-Refpages/   ← Khronos command and GLSL function reference pages
references/GLSL/              ← GLSL specification source and extension sources
references/VK-GL-CTS/         ← OpenGL and OpenGL ES conformance tests
references/OpenGL-Tutorials/  ← Runnable native OpenGL examples
references/Mesa/              ← Open-source OpenGL/GLES driver and state-tracker implementation
```

Use the separate `webgl` skill for the browser API. WebGL is based on OpenGL ES but adds browser-specific validation, security, and lifecycle rules.

## Choose the authoritative source

| Topic | Primary source |
|---|---|
| Core GL/GLES specifications | `references/OpenGL-Registry/specs/gl/` or `specs/es/` |
| C headers and exact declarations | `references/OpenGL-Registry/api/GL/` or `api/GLES*/` |
| API and enumerant registry | `references/OpenGL-Registry/xml/gl.xml` |
| Published GL/GLES extensions | `references/OpenGL-Registry/extensions/` |
| Per-command and GLSL built-in reference | `references/OpenGL-Refpages/gl4/`, `gl2.1/`, or `es*/` |
| GLSL source and newer shader extensions | `references/GLSL/chapters/`, `core.adoc`, and `extensions/` |
| Conformance tests | `references/VK-GL-CTS/external/openglcts/` and `modules/` |
| Driver behavior and implementation details | `references/Mesa/src/` |
| Example application patterns | `references/OpenGL-Tutorials/tutorial*/` |

Prefer Khronos specifications over refpages when precision matters. Treat tutorials as illustrative and Mesa as an implementation, not the definition of OpenGL.

## Answer API and extension questions

1. Identify the API family, version, profile, and platform binding: desktop GL versus GLES, core versus compatibility, and EGL/GLX/WGL/CGL when relevant.
2. Confirm the declaration and enum in the Registry headers or `xml/gl.xml`.
3. Read the matching specification section for state changes, errors, synchronization, and version/profile constraints.
4. Use Refpages for quick navigation, then confirm ambiguous language against the specification.
5. For extensions, read the extension document and its dependencies, interactions, and revision history.

## Answer GLSL questions

1. Identify the exact GLSL or GLSL ES version and enabled extensions.
2. Read the matching language specification in `OpenGL-Registry/specs/` and relevant source in `GLSL/`.
3. Cross-check built-ins in `OpenGL-Refpages` and compiler behavior in CTS or Mesa when needed.
4. Separate required language behavior from compiler- or driver-specific diagnostics.

## Debug implementation and rendering issues

1. Reduce the problem to the smallest relevant `OpenGL-Tutorials` or CTS pattern.
2. Check context version/profile, loader declarations, object lifetime, binding state, framebuffer completeness, shader compile/link logs, and GL errors.
3. Search CTS for the operation and expected result before declaring driver non-conformance.
4. Search Mesa only when the active driver or conceptual implementation path makes it relevant; identify the driver and state tracker used.
5. State when behavior is undefined, implementation-dependent, version-gated, or extension-gated.

## Work with conformance tests

1. Start with `references/VK-GL-CTS/external/openglcts/README.md` and the test modules matching the requested GL/GLES version.
2. Search test names and source for the API or feature, then follow framework helpers and generated cases.
3. Distinguish official CTS requirements from ordinary unit tests and Mesa regressions.
4. Use release tags or the user's target conformance version when exact certification behavior matters.

## Answering strategy

- Search or read local files before answering.
- Cite repository-relative files so the evidence is reproducible.
- Keep desktop GL, GLES, GLSL, platform bindings, and driver behavior distinct.
- Do not infer hardware or driver support from registry presence; query or verify the target system when support matters.
- If submodules are absent, run `git submodule update --init` from the skill directory before relying on memory. Do not add `--recursive`: these repos are read-only references and are never built, so nested build dependencies are pure overhead.
