# OpenGL-AGENTS

An agent skill that answers OpenGL and OpenGL ES questions by referencing locally cloned official
repositories, rather than relying solely on training data. It is agent-agnostic and works with any
coding agent that supports skills (Claude Code, Codex, etc.).

### Reference repos included

| Repo | Purpose |
|------|---------|
| `references/OpenGL-Registry` | Khronos GL/GLES specs, headers, extensions, and the XML registry |
| `references/OpenGL-Refpages` | Khronos command and GLSL function reference pages |
| `references/GLSL` | GLSL specification source and extension sources |
| `references/VK-GL-CTS` | OpenGL and OpenGL ES conformance tests |
| `references/OpenGL-Tutorials` | Runnable native OpenGL examples |
| `references/Mesa` | Open-source OpenGL/GLES driver and state-tracker implementation |

## Installation

Install once into the shared agent skills directory, then symlink it into each agent's skills folder.

The reference repos are git submodules. Initialize them one level deep only — they are read-only
references that are never built, so nested build dependencies are pure overhead:

```bash
git clone git@github.com:rygo6/OpenGL-AGENTS.git ~/.agents/skills/opengl
cd ~/.agents/skills/opengl
git submodule update --init
git submodule update --remote
```

Do not pass `--recursive` or clone with `--recurse-submodules`.

Then link it into the agents you use:

```bash
mkdir -p ~/.claude/skills ~/.codex/skills
ln -s ~/.agents/skills/opengl ~/.claude/skills/opengl
ln -s ~/.agents/skills/opengl ~/.codex/skills/opengl
```

On Windows, use `mklink /J` to create a junction instead (run in `cmd`, no admin rights needed):

```bat
mklink /J "%USERPROFILE%\.claude\skills\opengl" "%USERPROFILE%\.agents\skills\opengl"
mklink /J "%USERPROFILE%\.codex\skills\opengl"  "%USERPROFILE%\.agents\skills\opengl"
```

## Usage

Once installed, invoke `/opengl` from any agent that supports skills.

## Related skills

Use `webgl` for the browser API, `metal` for Apple Metal, and `vulkan` for Vulkan and MoltenVK.
