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
