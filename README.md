# 2023-Nanjing-Walk-Time

## access-walking-time-Table Schema (Columns)

| Column | Type | Description |
|---|---|---|
| `number` | int/float | Station identifier (ID). |
| `Exponnorm_Off_peak` | tuple / string | Exponentially modified normal (ExponNorm / EMG) fit parameters for **off-peak** data. Typically stored as a tuple `(K, loc, scale)` or equivalent. |
| `Exponnorm_Peak` | tuple / string | ExponNorm / EMG fit parameters for **peak** data. Typically stored as a tuple `(K, loc, scale)` or equivalent. |
| `Mean_OP` | float | Mean value of the fitted/observed distribution during **off-peak** (OP). |
| `Mean_p` | float | Mean value of the fitted/observed distribution during **peak**. |
| `flow` | float | Total passenger flow (e.g., aggregated volume for the station over the study period). |
| `Line` | string | Metro/rail line name or code that the station belongs to (e.g., `Line1`). |
| `label` | string | Station type label, typically one of: `High`, `Med`, `Low`. |
| `Off_peak_std_dev` | float | Standard deviation during **off-peak**. |
| `Peak_std_dev` | float | Standard deviation during **peak**. |
| `Off_peak_decay_rate` | float | Decay rate during **off-peak** (derived from the fitted distribution / tail behavior). |
| `Peak_decay_rate` | float | Decay rate during **peak** (derived from the fitted distribution / tail behavior). |


## egress-walking-time-Table Schema (Columns)

| Column (CN) | Column (EN suggestion) | Description |
|---|---|---|
| 站名 | `station_name` | Name of the station. |
| 车站编号 | `station_id` | Unique station identifier (ID/code). |
| 站型 | `station_category` | Station category/type used in the dataset context (e.g., operational or functional classification). |
| 车站站型 | `station_structure_type` | Station structural type classified by floor/level layout** (e.g., based on the number of levels, concourse/platform arrangement, underground vs. above-ground level configuration). |
| 拟合分布 | `fitted_distribution` | Name of the probability distribution used to fit the station’s data. One of: `exponnorm`, `burr`, `genhyperbolic`. |
| 指标 | `goodness_of_fit_metric` | Overall goodness-of-fit evaluation metric** used to assess the fitting quality (a comprehensive fit score/criterion). |
| 参数 | `params` | Distribution parameters of the fitted model, consistent with SciPy**’s parameterization for the specified distribution (`exponnorm`, `burr`, `genhyperbolic`). Typically recorded as an ordered tuple/list (see below). |

## Distribution Parameterization (SciPy-Compatible)

The `params` column stores the fitted parameters following SciPy’s conventions:

- **exponnorm** (`scipy.stats.exponnorm`):  
  `params = (K, loc, scale)`

- **burr** (`scipy.stats.burr` / Burr Type XII):  
  `params = (c, d, loc, scale)`

- **genhyperbolic** (`scipy.stats.genhyperbolic`):  
  `params = (p, a, b, loc, scale)`
