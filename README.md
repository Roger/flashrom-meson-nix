Patched version of [nixpkgs flashrom](https://github.com/NixOS/nixpkgs/blob/e7a4ed12aaff051818f1fc70ef19a306a46b504b/pkgs/tools/misc/flashrom/default.nix) compiled with meson.

Meson is needed to build fwupd with flashrom plugin.

## Example usage as an overlay, in a flake:

```nix
inputs = {
  flashrom-meson = {
    url = "github:roger/flashrom-meson-nix";
    flake = false;
  };
  ...
};
outputs = { flashrom-meson }:
  let overlay-replace-flashrom = final: prev: {
    flashrom = final.callPackage flashrom-meson {};
  };
  in {
    nixosConfigurations.host = nixpkgs.lib.nixosSystem {
      modules = [ overlay-replace-flashrom ];
      ...
    };
  ...
};
```
