# intestinal-fibroblast-protocol
## Overview
**CellProfiler pipelines quantifying activation markers (α-SMA, FAP, Vinculin) and cell counts** from the study:  
*[Developing a Protocol to Counteract Spontaneous In vitro Activation of Intestinal Fibroblasts Using Design of Experiments](https://www.researchsquare.com/article/rs-7677632/v1)*
This paper investigates an _in vitro_ approach to induce inactivated culture of colonic fibroblasts on TCPS. 

## Pipelines 

| Pipeline | Purpose | Input Channels | Processing | Output |
|----------|---------|----------------|------------|--------|
| `αSMA-intensity, CellProfiler Pipeline-for validation` | αSMA intensity per cell | CH1: DAPI, CH3: αSMA | Identify nuclei (DAPI), expand to cytoplasm, measure CH3 intensity | CSV: Integrated intensity per cell → average per well |
| `Vinculin-FAP, CellProfiler Pipeline` | Vinculin + FAP intensity per cell | CH1: DAPI, CH2: Vinculin/FAP | Nuclei → cytoplasm expansion, measure marker intensity | CSV: Integrated intensity per cell → average per well |
| `dapi count, CellProfiler Pipeline-for 20x` | Nuclei counting at 20x | CH1: DAPI only | IdentifyPrimaryObjects on DAPI channel | CSV: Nuclei count → sum per well|
| `Live count, CellProfiler Pipeline` | Live/dead cell counting | Live cell count (run separately for dead cells) | IdentifyPrimaryObjects on live/dead channel | CSV: Live cell count per field → sum per well → run again for dead cells |

## Workflow Notes
- **Dual-channel pipelines** (αSMA, Vinculin, FAP): DAPI CH1 identifies nuclei → cytoplasm expansion → measure marker intensity in CH2/3
- **Live-dead**: Run pipeline twice—once per channel (live, then dead)
- **Final reporting**: Average CSV intensity values per cell per well in GraphPad Prism

## Requirements
- CellProfiler 4.2+
- Input: TIFF images from [microscope]
- Output: CSV measurements + plots

## Usage
1. Open pipeline in CellProfiler
2. Load image folder
3. Run analysis → Check `ExportToSpreadsheet` module
4. Visualize in GraphPad Prism 









