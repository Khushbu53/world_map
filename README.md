# Khushbu-demo
# world_map_geopandas.py
"""
Plot a world map using geopandas' built-in Natural Earth dataset.
Requires: geopandas, matplotlib
"""

import sys

def plot_world_map(save_as=None, color_land="#d9d9d9", edgecolor="#333333", figsize=(14,8)):
    try:
        import geopandas as gpd
        import matplotlib.pyplot as plt
    except ImportError as e:
        raise ImportError(
            "Required packages missing. Install with:\n"
            "    pip install geopandas matplotlib\n"
            "Then re-run this script."
        ) from e

    # load Natural Earth low-res dataset bundled with geopandas
    world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))

    fig, ax = plt.subplots(figsize=figsize)
    world.plot(ax=ax, color=color_land, edgecolor=edgecolor, linewidth=0.5)

    # Optional styling
    ax.set_title("World map (Natural Earth - low resolution)", fontsize=16)
    ax.set_axis_off()  # hide axes (lat/lon ticks)
    plt.tight_layout()

    if save_as:
        fig.savefig(save_as, dpi=300, bbox_inches='tight')
        print(f"Saved map to {save_as}")

    plt.show()

if __name__ == "__main__":
    plot_world_map(save_as="world_map.png")

