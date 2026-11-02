# godot-combat-tuning-workbench

A Claude skill for tuning combat moves, visual effects (VFX), animation timing and enemy AI in Godot 4 projects.

The workflow has three steps:

1. **See it first:** show the move as a diagram or timeline before changing code.
2. **Tune it by hand:** build a preview workbench with sliders, layers, presets, before/after comparison and JSON export.
3. **Prove it in the game:** run photo tours, simulated-player tests and an optional director review.

The skill is written in English by default, with a Portuguese version included in the same file.

## License

Released under the [MIT License](LICENSE).

## Example usage

Ask Claude for a change in plain words, for example:

> Make the knight's dash attack a bit faster, with a 0.25 s warning and a short wind trail. Build a preview workbench first.

Claude then:

1. Shows a timeline of the move (warning, active, recovery) for you to approve.
2. Builds a preview page with sliders for the trail, timing and hit area. The control panel sits beside the preview.
3. After you export the JSON from the workbench and paste it back, applies the same numbers to the game script and runs a photo tour to check the result.

A project can describe its own paths and rules in a `tuning-config.json` file at the project root:

```json
{
  "engine": "Godot 4.x",
  "project_root": "/absolute/path/to/your-game",
  "godot_dir": "godot",
  "test_scenes_dir": "scenes/tests",
  "test_scripts_dir": "tests",
  "output_dir": "_tuning_tmp",
  "camera_shake": false,
  "secret_names_never_log": [],
  "paid_generation_requires_approval": true
}
```

With `camera_shake` set to `false`, impacts stay soft.

## Example: an ice mage's wave attack

This standard example uses a made-up ice mage who casts a row of ice waves across the ground. Changing the numbers changes the shape of the attack.

**Controls used in the example:**

- **Count:** how many waves appear.
- **Spacing:** the distance between waves.
- **Height:** how tall each wave rises.
- **Curve:** how round (high) or sharp (low) the wave edge is.
- **Tilt:** how much the wave leans.
- **Fade:** how quickly the wave turns transparent.

**Three presets** shown in the demo:

| Preset | Count | Spacing | Height | Curve | Tilt | Fade |
|---|---|---|---|---|---|---|
| `ice-wave-v1` | 3 | 48 | 36 | 0.7 | 12 | 0.4 |
| `ice-wave-v2` | 5 | 36 | 70 | 0.2 | -10 | 0.2 |
| `ice-spike-v3` | 1 | 20 | 100 | 0.9 | 0 | 0.1 |

A preset saved as JSON looks like this:

```json
{
  "name": "ice-wave-v2",
  "layers": {
    "wave": { "enabled": true, "count": 5, "spacing": 36, "height": 70, "curve": 0.2, "tilt": -10, "fade": 0.2 }
  }
}
```

**Demo video:** [ice-mage-wave-demo.mp4](docs/ice-mage-demo/ice-mage-wave-demo.mp4) (13 seconds, shows the four presets in turn: frost arc, crystal spikes, shard burst and cracked ice slab).

**Interactive demo:** open [docs/ice-mage-demo/index.html](docs/ice-mage-demo/index.html) in a browser to see the controls working. It includes four shapes (frost arc, crystal spikes, shard burst, ice slab), four colors (or a custom pair), and shader options for cracks, glow, sparkle and edge lines.

**Shader and effect sources:** [docs/shader-index.md](docs/shader-index.md)
