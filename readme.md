# Demographic Geofencing: District & Pincode Clustering 

## Project Overview
This project focuses on analyzing Aadhar demographic data to identify natural groupings of districts and pincodes based on the age distribution of their populations. By applying unsupervised learning techniques, specifically K-Means clustering, we aim to uncover distinct demographic profiles across different geographical units, which can inform targeted resource allocation, urban planning, and policy-making.

## Goal
The primary goal is to cluster Indian districts and pincodes into demographically similar groups using the proportion of individuals in two key age brackets: 5-17 years (youth) and 17+ years (adults). This helps in understanding the diverse demographic landscapes and supports data-driven decision-making.

## Data
The project utilizes Aadhar demographic data, specifically focusing on the counts of `demo_age_5_17` and `demo_age_17_` for various districts and pincodes. The data was loaded from multiple CSV files and combined into a single DataFrame.

### Key Data Derivations:
*   `total_demographic`: Sum of `demo_age_5_17` and `demo_age_17_`.
*   `prop_age_5_17`: Proportion of population aged 5-17.
*   `prop_age_17_`: Proportion of population aged 17+.

## Methodology

### 1. Data Loading and Preprocessing
*   Multiple CSV files containing Aadhar demographic data were loaded and concatenated.
*   `date` column was converted to datetime objects.
*   Proportional age distribution features (`prop_age_5_17`, `prop_age_17_`) were calculated at both district and pincode levels.
*   District names were cleaned to handle encoding issues.

### 2. Exploratory Data Analysis (Initial Visualizations)
Before clustering, an initial analysis was performed to identify the top and bottom 5 districts/pincodes based on the proportion of age groups, providing an early glimpse into the data's variability.

### 3. Clustering Analysis (K-Means)
*   **Feature Selection**: `district_prop_age_5_17`, `district_prop_age_17_` for districts and `pincode_prop_age_5_17`, `pincode_prop_age_17_` for pincodes were selected as features.
*   **Scaling**: Features were scaled using `StandardScaler` to ensure that all features contribute equally to the distance calculation in K-Means.
*   **Optimal K Determination**: The Elbow Method (using `KElbowVisualizer` from Yellowbrick) was employed to determine the optimal number of clusters (`k`) for both district and pincode data. Based on visual inspection, `k=3` was chosen for districts and `k=4` for pincodes.
*   **Model Application**: K-Means clustering was applied to the scaled data, and cluster labels were assigned back to the original DataFrames (`district_demographics_combined` and `pincode_demographics_combined`).

### 4. Visualization of Cluster Results
Scatter plots were generated to visualize the clusters, showing the proportion of age 5-17 vs. age 17+ for each geographical unit, colored by their assigned cluster. Unscaled cluster centers were overlaid on these plots to represent the average demographic profile of each cluster.

## Key Findings & Cluster Profiles

The clustering revealed distinct demographic profiles:

### District Cluster Profiles:
*   **Cluster 0 (Balanced/Adult-Leaning)**: Relatively balanced, with a clear majority in the adult population (~84.7% Age 17+).
*   **Cluster 1 (Adult-Dominant)**: High adult population (~93.4% Age 17+), possibly indicating mature or business-centric areas.
*   **Cluster 2 (Youth-Dominant)**: Very high proportion of younger age group (~74.6% Age 5-17), suggesting areas with educational institutions or young populations.

### Pincode Cluster Profiles:
*   **Cluster 0 (Adult-Leaning)**: Similar to District Cluster 0, with a noticeable adult majority (~87.8% Age 17+).
*   **Cluster 1 (Highly Adult-Dominant)**: Overwhelmingly adult population (~94.1% Age 17+), potentially urbanized or specialized adult living zones.
*   **Cluster 2 (Youth-Balanced)**: Higher proportion of younger age group (~21.0% Age 5-17) compared to Clusters 0 and 1, indicating family-oriented areas.
*   **Cluster 3 (Highly Youth-Dominant)**: Predominantly young population (~82.5% Age 5-17), likely dedicated educational areas or densely populated residential areas with young families.

## Use Cases and Applications

These insights can be leveraged for:

*   **Targeted Resource Allocation**: Directing resources like schools, healthcare facilities, and child development programs to youth-dominant areas, and adult healthcare/vocational training to adult-dominant areas.
*   **Urban Planning**: Guiding housing policies (e.g., family-sized homes in youth-dominant areas, smaller units in adult-dominant areas) and planning public services.
*   **Policy-Making**: Crafting demographic-specific policies, such as promoting early childhood education in youth-dominant clusters or addressing senior welfare in adult-dominant ones.

## Limitations

While powerful, the analysis is based on aggregated demographic data. This means it provides macro-level insights and cannot be used for individual-level predictions or to infer individual behaviors. However, it effectively segments geographical units to understand their overarching demographic structures.

## Technologies Used
*   Python
*   Pandas (for data manipulation)
*   Matplotlib (for plotting)
*   Seaborn (for enhanced visualizations)
*   Scikit-learn (for clustering and scaling)
*   Yellowbrick (for K-Elbow Visualizer)
