# Syntheticus Templates
A repository collecting templates for configuration files and metadata files; all testable through the Syntheticus API in Notebooks

# YAML Configuration File Documentation

This YAML configuration file is designed to configure a machine learning pipeline. The configuration file is divided into several steps, each representing a stage in the pipeline.

## Configuration Structure
The configuration file has the following main sections:
1. `'config_version'`: Specifies the version of the configuration file format.
2. `'config_name'`: A name for the configuration.
3. `'config_steps'`: A list of steps in the pipeline, which may include:
    * `'data'`
    * `'transform'`
    * `'model'`
    * `'sample'`
    * `'metrics'`

## Data
In the `'data'` step, you can specify the dataset version to be used in the pipeline.

```yaml
data:
  dataset_version: # Dataset Name
```

## Transforms

The available transformations are defined in the `transform` section of the YAML configuration file. Each transformation has a `type` and `parameters`.

### Drop

Remove specified columns from the data.

```yaml
- type: drop
  parameters:
    columns: ['column_name1', 'column_name2']
```

### Fake
Replace values in specified columns with fake data.

```yaml
- type: fake
  parameters:
    columns: ['column_name1', 'column_name2']
    providers: ['provider1', 'provider2']
    seed: seed_value
    locale: ['locale1', 'locale2']
    unique: boolean_value
```

### Hash
Replace values in specified columns with hash of the value.

```yaml
- type: hash
  parameters:
    columns: ['column_name1', 'column_name2']
    hash_type: 'hash_type'
    salt: 'salt'
```

### Number shift
Shift numeric values in specified columns by a random amount within a specified range.

```yaml
- type: number_shift
  parameters:
    columns: ['column_name1', 'column_name2']
    min: minimum_shift_value
    max: maximum_shift_value
    precision: precision_value
```

### Date shift
Shift date values in specified columns by a random amount within a specified range.

```yaml
- type: date_shift
  parameters:
    columns: ['column_name1', 'column_name2']
    min: minimum_shift_value
    max: maximum_shift_value
    formats: date_format
```

### Generalize
Replace values in specified columns with generalized versions.

```yaml
- type: generalize
  parameters:
    columns: ['column_name1', 'column_name2']
    ranges: [range1, range2]
    labels: ['label1', 'label2']
```

### Shuffle
Randomly shuffle values in specified columns.

```yaml
- type: shuffle
  parameters:
    columns: ['column_name1', 'column_name2']
```

### K-anonimity
Apply K-Anonymity to specified columns.

```yaml
- type: k_anonymity
  parameters:
    k: k_value
    quasi_identifiers: ['column_name1', 'column_name2']
    generalization_columns:
      column_name3:
        ranges: [range1, range2]
        labels: ['label1', 'label2']
```

### L-Diversity
Apply L-Diversity to specified columns.

```yaml
- type: l_diversity
  parameters:
    l: l_value
    columns: ['column_name1', 'column_name2']
    quasi_identifiers: ['column_name3', 'column_name4']
```

### T-Closeness
Apply T-Closeness to specified columns.

```yaml
- type: t_closeness
  parameters:
    columns: ['column_name1', 'column_name2']
    quasi_identifiers: ['column_name3', 'column_name4']
    t: t_value
```

### Perturbation
Apply noise to numeric values in specified columns.

```yaml
- type: perturbation
  parameters:
    columns: ['column_name1', 'column_name2']
    noise_scale: noise_scale_value
```

### Tokenization
Replace unique values in specified columns with a unique token.

```yaml
- type: tokenization
  parameters:
    columns: ['column_name1', 'column_name2']
```

### Configuration Parameters

Each transformation type accepts a different set of parameters. Here are the descriptions for each parameter:

* `'columns'`: List of column names to be transformed.
* `'providers'`: List of faker providers to use for generating fake data.
* `'seed'`: Seed for the random number generator.
* `'locale'`: List of locales to use for generating fake data.
* `'unique'`: Boolean to determine if the fake data should be unique.
* `'hash_type'`: The type of hash function to use. Options are 'md5', 'sha256', and 'sha512'.
* `'salt'`: Salt string to add to the data before hashing.
* `'min'`: Minimum shift for number or date shift.
* `'max'`: Maximum shift for number or date shift.
* `'precision'`: Number of decimal places to round shifted numbers to.
* `'formats'`: Format to parse dates in.
* `'ranges'`: List of ranges to use for generalization.
* `'labels'`: Labels corresponding to each range in generalization.
* `'k'`:  k value for k-anonymity.
* `'quasi_identifiers'`: List of quasi-identifier columns for k-anonymity, l-diversity, and t-closeness.
* `'generalization_columns'`: Mapping of columns to their generalization ranges and labels for k-anonymity.
* `'l'`: l value for l-diversity.
* `'t'`: t value for t-closeness.
* `'noise_scale'`: Scale of the normal distribution to generate noise from for perturbation.

Please refer to the specific transformation sections above for how to use these parameters in the YAML configuration file.

## Model
The `'model'`step is reserved for future use.

## Sample
In the `'sample'` step, you can specify the number of rows to sample from the transformed dataset.

```yaml
sample:
  number_of_rows: ''
```

## Metrics

In the `'metrics'` step, you can define a series of metrics to be computed on the transformed dataset. Each metric is defined by its type and parameters.

Supported metrics:
```yaml
metrics:
  - name: # Table Name
      column_plot: ['column1', 'column2', ...]
      column_pair_plot: [['column1','column2'], ['column1','column3'], ...]
      cap: [
        [
          ['column1, ...'],    # key_fields
          ['column4, ...']     # sensitive_fields
        ]
      ]
```

## Usage
To use this YAML configuration file, save it as a file (e.g., config.yaml) and pass it to your machine learning pipeline as an input. The pipeline will then execute the specified steps in order, applying the specified transformations and computing the specified metrics.



