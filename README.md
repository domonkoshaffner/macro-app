# Macro App

A Jupyter notebook that reads a Google Sheets food log and calculates daily calories, macros, and weekly averages.

## Local configuration

Install the Python libraries imported by `food_calc.ipynb` in your notebook environment. Create a Google service account with access to the Sheets API, keep its JSON key at `.local/service-account.json`, and share your spreadsheet with that service account as a viewer.

Set the spreadsheet ID in your environment before starting Jupyter:

```sh
export MACRO_APP_SPREADSHEET_ID='your-spreadsheet-id'
```

The ID is the value between `/d/` and `/edit` in the spreadsheet URL. These environment variables control the remaining settings:

| Variable | Default |
|---|---|
| `GOOGLE_APPLICATION_CREDENTIALS` | `.local/service-account.json` |
| `MACRO_APP_LOG_WORKSHEET` | `daily_log` |
| `MACRO_APP_MACROS_WORKSHEET` | `macros` |
| `MACRO_APP_KCAL_CONFIG` | `kcal.yaml` |

The tracked `kcal.yaml` contains synthetic demonstration values. Copy it to `.local/kcal.yaml`, adjust the activity names and rates there, and set `MACRO_APP_KCAL_CONFIG` to that path for your own configuration. Activity names in the daily log must match the configuration keys.

The `.local/` directory is ignored by Git. Keep account settings, credentials, and personal data there or outside the repository. Notebook results contain spreadsheet data, so clear all outputs before committing the notebook.

## Input sheet layout

All examples below are artificial. Replace the placeholders with your own entries in Google Sheets. The table headings describe the column order; enter only data rows in the worksheets.

### Daily log: `daily_log`

Use one `general`, `breakfast`, `lunch`, and `dinner` row per date, formatted as `YYYY/MM/DD`. The first two columns are the date and row type. Meal rows use the remaining columns for `item - quantity` entries.

| Date | Type | Mass / food | Workout / food | Phase / food | Expected / food | Cardio / food |
|---|---|---|---|---|---|---|
| `YYYY/MM/DD` | general | `<mass> kg` | demo_workout | demo_phase | `<target> kcal` | `demo_cardio - <minutes> min` |
| `YYYY/MM/DD` | breakfast | demo_food - 100g | | | | |
| `YYYY/MM/DD` | lunch | demo_food - 100g | | | | |
| `YYYY/MM/DD` | dinner | demo_food - 100g | | | | |

### Food reference: `macros`

The column order must match the fields used by the notebook. The values here describe an invented example food.

| Item | Quantity | Calories | Carbs | Fat | Protein | Sugar | Fiber | Usual amount | Type |
|---|---|---|---:|---:|---:|---:|---:|---|---|
| demo_food | 100 g | 40 kcal | 10 | 0 | 0 | 0 | 0 | 100 g | demo |

## Results

Run the notebook from top to bottom to display the summary table. It includes meal totals, activity estimates, macronutrient proportions, and weekly averages. The existing table labels put the workout name under `Day` and the activity duration under `Workout`.
