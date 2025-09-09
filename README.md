# Task A: Use the provided cleaning code (or notebook) to generate 'inventory_dataset.csv'
Notes:
- Performs stronger normalization (grade tightening, finish extraction from description, numeric coercions) and adds a `Source` column.

# Task B:

This project implements a pipeline for **Scenario B**: matching RFQs based on grades, dimensions, and categorical properties.

## Steps

1. **Load & Clean**
   - Normalize `grade` (uppercase, trim, remove spaces around + and -).
   - Ensure consistent reference column (`Grade/Material`).

2. **Enrichment**
   - Join RFQs with reference_properties.tsv on normalized grade.
   - Keep nulls if no match (documenting that not all grades may exist in reference).

3. **Feature Engineering**
   - Dimensions converted to intervals (`min`/`max`).
   - If only one bound is provided, fill the missing one with the available value.
   - Categories: similarity = 1 if exact match (case-insensitive), else 0.

4. **Similarity Calculation**
   - **Interval overlap**: Intersection-over-Union (IoU).
   - **Categorical similarity**: exact matches of `coating`, `finish`, `form`, `surface_type`.
   - **Grade similarity**: based on tensile and yield strength overlaps.
   - Aggregate score = `0.4 * dimension + 0.3 * categorical + 0.3 * grade`.

5. **Output**
   - `rfq_enriched.csv`: RFQs with reference enrichment.
   - `top3.csv`: top-3 most similar RFQs per line.

## Files
- `case_assessment_vanilla_steel_scenario_a`
- `case_assessment_vanilla_steel_scenario_b`
- `run_task_b.ipynb`: notebook to execute task b flow.




