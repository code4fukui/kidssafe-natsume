# kidssafe-natsume

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A civic tech project by Code for Fukui creating a community safety map for children in the Natsume district of Fukui City, Japan. It identifies and maps local points of concern to enhance child safety.

## Demo

https://code4fukui.github.io/kidssafe-natsume/

## Features

-   **Interactive Map**: Displays local safety information (e.g., "Children's Shelter 110" houses, potential hazards) with custom icons.
-   **Detailed Information**: Clicking a pin on the map reveals details, such as the nature of a concern and proposed improvements, directly from the data.
-   **Data-Driven**: All map points are managed through simple, easy-to-edit CSV files.
-   **Adaptable**: Easily reusable for other communities by changing the configuration and data files. No backend required.
-   **Precise Locations**: Uses [Geo3x3](https://geo3x3.com/) for an efficient and accurate way to encode and share geographic coordinates.

## How to Adapt for Your Area

This project is designed to be easily configured for any district.

1.  **Fork or Clone**: Get a copy of the repository.
2.  **Customize Metadata**: Edit `index.html` to change the main title (`<title>`) and the header text.
3.  **Configure Layers**: Modify `index.csv` to define your map layers. Each row links a layer name, its data file, and a display icon.
4.  **Add Data**: Create or edit CSV files with your local safety data (e.g., in the `kidssafe/` directory). See the Data Structure section for details.
5.  **Add Icons**: Place your custom map icons in the `icon/` directory.
6.  **Publish**: Deploy the static site to a host like GitHub Pages.

## Development

This project is a static website and requires no build step. For local testing, you need a simple web server to handle the module imports correctly.

[Deno](https://deno.land/) provides a one-command web server:

```bash
# Run from the project's root directory
deno run --allow-net --allow-read https://deno.land/std/http/file_server.ts
```

## Data Structure

The map is configured and populated using CSV files.

### Main Configuration (`index.csv`)

This file defines the data layers that appear on the map.

| Column | Description                                                  | Example                  |
| :----- | :----------------------------------------------------------- | :----------------------- |
| `name` | The display name for the data layer.                         | `100当番の家`            |
| `fn`     | The path to the CSV file containing the location data.       | `house100.csv`           |
| `icon`   | The filename of the icon (in the `icon/` directory) for this layer. | `house110_icon.png`      |

### Location Data (e.g., `kidssafe/田ノ頭町.csv`)

These files contain the individual points for a layer.

-   The first row defines the headers. These headers are used as field labels in the pop-up info box on the map.
-   A `Geo3x3` column is required to position the point on the map.

**Example (`kidssafe/田ノ頭町.csv`):**

```csv
危険箇所・気がかりな点,改善案,Geo3x3
田ノ頭町内のため池。柵は設置されているが、転落等の注意が必要。,,E913873765598238
```

## Attribution

-   **Map Tiles**: [Geospatial Information Authority of Japan (GSI)](https://maps.gsi.go.jp/development/ichiran.html)

## License

MIT License — see [LICENSE](LICENSE).