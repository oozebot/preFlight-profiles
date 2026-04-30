# preFlight Profiles

Printer and filament profiles for [preFlight](https://preflight3d.com), a 3D printing slicer.

Vendors and community members are welcome to submit pull requests to add new printers, update existing profiles, or improve settings.

## Structure

```
index.json           # Master index of all vendors and their current version
Filaments.ini        # Unified filament database (all vendors, all types)
{Vendor}.ini         # Vendor profile (printer models, print settings, printer settings)
{Vendor}/            # Resource folder (thumbnails, bed models, bed textures)
```

Each vendor has a single `.ini` file containing all of their printer definitions, print settings, and printer settings. Filaments are in a separate unified `Filaments.ini` database. The corresponding vendor folder contains any referenced resources like printer thumbnails, bed model STLs, and bed texture SVGs.

## Contributing

### Adding a New Vendor

1. Create a `{VendorName}.ini` following the format of existing vendor profiles
2. Create a `{VendorName}/` folder with your printer thumbnails, bed models, and bed textures
3. Add your vendor and version to `index.json`
4. Submit a pull request

### Updating an Existing Profile

1. Update the `.ini` file with your changes
2. Bump the `config_version` in the `[vendor]` section of the `.ini`
3. Update the version in `index.json` to match
4. Add or replace any new resource files in the vendor folder
5. Submit a pull request

### Profile Format

The `[vendor]` section at the top of each `.ini` defines the vendor metadata:

```ini
[vendor]
name = Your Company Name
config_version = 1.0.0
```

Printer models are defined with `[printer_model:ID]` sections:

```ini
[printer_model:MY_PRINTER]
name = My Printer Name
variants = 0.4; 0.6; 0.8
technology = FFF
family = MyFamily
bed_model = my_printer_bed.stl
bed_texture = my_printer_bed.svg
thumbnail = MY_PRINTER_thumbnail.png
```

Resources referenced by `bed_model`, `bed_texture`, and `thumbnail` must be placed in the vendor's resource folder.

### Guidelines

- **Thumbnails** should be PNG, roughly 160x120 pixels
- **Bed models** should be STL files representing the print bed
- **Bed textures** should be SVG files representing the bed surface appearance
- **Test your profiles** before submitting - load them in preFlight and verify they produce good results
- **Bump the version** in both the `.ini` and `index.json` with every change

## License

Profiles in this repository are provided for use with preFlight under [AGPLv3](https://www.gnu.org/licenses/agpl-3.0.en.html).
