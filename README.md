# Infrastructure Analysis Team - Instance Segmentation Project

## Project Overview

The Infrastructure Analysis Team is tasked with developing a instance segmentation model for identifying infrastructure elements in high-resolution orthomosaic imagery for urban planning and infrastructure monitoring across the Nepal Valley region.

## Objective

Develop an instance segmentation model capable of accurately detecting and segmenting the following infrastructure classes from TIFF orthomosaic imagery:

- **Buildings**: Residential, commercial, and institutional structures
- **Roads**: Paved and unpaved transportation networks
- **Bridges**: River crossings and elevated infrastructure
- **Temples**: Religious and cultural heritage structures
- **Irrigation Channels**: Water distribution infrastructure

The model must distinguish between individual instances of each class (e.g., separate buildings) rather than treating all buildings as a single segmented region.

## Technical Context

### Understanding Orthomosaic Data

Please use this georeferenced TIFF orthomosaics generated from drone imagery.

**Full orthomosaics (Google Drive):**

* Pre-flood: **[[Drive link – pre]](https://drive.google.com/file/d/1WbqOriGyrFopdbPpITrsnGianvR4gGJw/view?usp=share_link)**
* Post-flood: **[[Drive link – post]](https://drive.google.com/file/d/1kAeYCiZ-L6RbOcBz9znynw-wKCsRxE-Q/view?usp=share_link)**


### Instance Segmentation Approach

Instance segmentation combines object detection and semantic segmentation to identify and delineate individual object instances. Recommended architectures include:

- **Mask R-CNN**: Standard baseline, proven on aerial imagery datasets
- **Cascade Mask R-CNN**: Multi-stage refinement for precise boundaries
- **HTC (Hybrid Task Cascade)**: Superior to Cascade Mask R-CNN for complex scenes
- **PointRend**: Precise boundary delineation for irregular infrastructure shapes
- **Mask2Former**: Universal segmentation architecture with strong aerial imagery performance
- **QueryInst**: Query-based instance segmentation, efficient for dense scenes
- **SOLOv2**: Direct instance segmentation, good for real-time inference on tiles

## Annotation Strategy

The team has flexibility in annotation methodology:

### Option 1: Tile-Based Annotation
- Divide the large orthomosaic into manageable tiles (e.g., 1024x1024 or 2048x2048 pixels)
- Annotate each tile independently
- Advantages: Easier handling, standard annotation tools compatible
- Considerations: Edge cases where objects span tile boundaries

### Option 2: Full Orthomosaic Annotation
- Annotate directly on the full-resolution orthomosaic
- Requires specialized tools (QGIS with annotation plugins, Label Studio with geospatial support)
- Advantages: Maintains spatial context, no boundary artifacts
- Considerations: Resource-intensive, requires robust annotation infrastructure

### Recommended Tools
- **Label Studio**: Web-based annotation with geospatial capabilities
- **CVAT**: Computer Vision Annotation Tool with polygon support
- **QGIS + Plugin**: For direct annotation on georeferenced imagery
- **Roboflow**: Annotation platform with tile management features

## Deliverables

### 1. Annotated Dataset
- Complete annotations for all five infrastructure classes
- Annotations in COCO format or similar instance segmentation standard
- Metadata file documenting:
  - Total instances per class
  - Annotation methodology (tiled vs. full)
  - Pixel resolution and coordinate reference system
  - Train/validation/test splits

### 2. Trained Instance Segmentation Model
- Model weights and configuration files
- Training logs and performance metrics (mAP, precision, recall per class)
- Inference script for deployment
- Model architecture documentation

### 3. Evaluation Report
Document containing:
- **Quantitative Metrics**: mAP@0.5, mAP@0.75, per-class performance
- **Qualitative Analysis**: Visual examples of successful detections and failure cases
- **Methodology**: Training parameters, data augmentation strategies, preprocessing pipeline
- **Challenges Encountered**: Issues with class imbalance, annotation ambiguities, computational constraints
- **Recommendations**: Suggestions for model improvement and future iterations

### 4. Inference Pipeline
- End-to-end pipeline for processing new orthomosaics
- Tiling strategy for large-format inputs
- Post-processing logic (non-maximum suppression, boundary handling)
- Output format: GeoJSON or Shapefile with instance polygons and class labels

### 5. Technical Documentation
- **README**: Setup instructions, environment requirements, usage examples
- **Code Documentation**: Inline comments and docstrings
- **Requirements File**: All dependencies with version specifications
- **Deployment Guide**: Instructions for model deployment in production environments

## Quality Assurance

### Model Performance Targets
- **Overall mAP@0.5**: ≥ 0.70
- **Per-Class mAP@0.5**: ≥ 0.60 for all classes
- **Inference Time**: < 10 seconds per 1024x1024 tile on GPU

## Key Considerations

**Class Imbalance**: Some infrastructure types may be rare (e.g., bridges, temples). Consider data augmentation, weighted loss functions, or synthetic data generation.

**Annotation Consistency**: Establish clear guidelines for boundary cases (e.g., partially visible structures, overlapping instances).

**Geospatial Accuracy**: Ensure output polygons maintain geographic accuracy for downstream GIS integration.

**Scalability**: Design the inference pipeline to handle arbitrarily large orthomosaics through efficient tiling and batch processing.
