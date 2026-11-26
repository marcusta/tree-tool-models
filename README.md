# tree-tool-models

Trees people share for [tree-tool](https://github.com/marcusta/tree-tool)
([live](https://marcusta.github.io/tree-tool/)). A model is a tree's settings, plus any textures and shader profile of its
own. Anyone can add one through a pull request.

## A model

One folder per model, `models/<id>/` (`id`: lower case letters, digits and `-`):

| File | |
|---|---|
| `model.json` | Required. See below. |
| `preview.png` | A picture of the tree, at most 1024 px. The app makes it. |
| textures (`*.png`, `*.jpg`) | Optional. Your own pictures for texture slots, at most 2048 px. |
| `profile.json` | Optional. A shader profile for your own shader, as the app loads it. |

```json
{
  "name": "Windswept coastal pine",
  "description": "Scots pine leaning away from the sea, high uneven crown.",
  "author": "Your name",
  "license": "CC0-1.0",
  "source": "https://example.com/where-the-textures-come-from",
  "tree": { "species": "pine", "preset": "windswept", "seed": 7, "changes": { "limbs.windBias": 0.6 } },
  "textures": { "bark.albedo": "bark.png" },
  "profile": "profile.json"
}
```

`tree` is the app's export settings: species, preset, seed and the sliders that differ from the preset. `textures`
maps a texture slot to a file in the folder. `source` is required for CC BY and CC BY-SA.

## Licences

Everything in a model's folder goes out under the model's `license`, and the app puts it into the `.unitypackage`
files people download. So a file may only come in when its licence allows passing it on as a file.

| Allowed `license` | |
|---|---|
| `CC0-1.0` | No conditions. Your own work, or for example ambientCG or Poly Haven. |
| `CC-BY-4.0` | `author` and `source` must name who made it and where it comes from. |
| `CC-BY-SA-4.0` | As CC BY; what builds on it is shared under the same licence. |

Not allowed:

- Files from Unity Asset Store packs (NatureManufacture, Forst and the like), Fab, Quixel or Megascans. Their licences
  allow using them in your own projects, not passing the files on. The app refers to such packs by GUID instead, so
  the tree finds them in a Unity project that has the pack.
- CC BY-ND (no changes allowed, and a tree built on a picture is a change) and CC BY-NC (people build courses they sell).
- Anything you are not sure about.

## Adding a model

The easy way is in the app: make the tree, open **Share this tree with everyone**, fill in name, author, licence and
source, and press **Check and prepare**. It runs the same check as this repo's pull requests, renders `preview.png`,
and gives you the files and a link to GitHub's upload page for `models/<id>/`. Drop the files there and choose
**Propose changes**: GitHub makes your copy of the repo and opens the pull request.

By hand: fork this repo, add `models/<id>/` with the files above and open a pull request. Fill in its checklist.

Every pull request is checked by `.github/workflows/models.yml` with tree-tool's own check
(`bun scripts/models.ts check models` in [tree-tool](https://github.com/marcusta/tree-tool)). A maintainer reviews
and merges it; on `main` the workflow publishes `index.json` and the folders on
<https://marcusta.github.io/tree-tool-models/>, where the app reads them.

To check locally, with tree-tool checked out beside this repo:

```sh
bun ../tree-tool/scripts/models.ts check models
```
