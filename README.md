# Report Widget Creation

The API endpoints are located within the `Reports/Reporting Dashboard` collection folder.

## Create a report Widget

## Step 1: Define the Widget Type
  
### Customize Your Widget
  If you want to create a custom widget, you can override the default values by providing additional configurations. You can customize:
  - `Widget Name`
  - `Chart Style`: (eg., color and type)
  - `Report Type`: (e.g., "Tasks", "Projects", etc.)
  - `Data Labels`: (whether to display data labels)
  - `Chart Axes`: (xAxis and yAxis)
 
  Example of a Customized Widget (Tasks):
  ```json
  {
    "name": "My Custom Widget",
    "chartDetails": {
      "chartStyle": { "color": "#A69FF3", "type": "Bar" },
      "reportOn": "Tasks",
      "includeTasksFrom": ["My workspace"],
      "showDataLabels": true
    },
    "chartAxes": {
      "xAxis": "Creator",
      "yAxis": "Task count"
    }
  }
  ```

  Example of a Customized Widget (Projects):
  ```json
  {
    "name": "My Custom Widget",
    "chartDetails": {
      "chartStyle": { "color": "#A69FF3", "type": "Bar" },
      "reportOn": "Projects",
      "includeTasksFrom": ["My workspace"],
      "showDataLabels": true
    },
    "chartAxes": {
      "xAxis": "Project owner",
      "yAxis": "Project count"
    }
  }
  ```

## Widget Types and Valid Values
  The following valid values are predefined for certain fields:
  - `VALID CHART TYPES`: ['Bar', 'Stacked bar', 'Grouped bar', 'Line', 'Burnup', 'Burndown', 'Donut', 'Number', 'Lollipop']
  - `VALID REPORT ON`: ['Tasks', 'Projects', 'Portfolios', 'Goals']
  - `VALID INCLUDE TASKS FROM`: ['My workspace', 'Teams', 'Portfolios', 'Projects owned by', 'Specific projects']
  - `VALID X AXIS (Report on: Task)`: ['Assignee', 'Creator', 'Custom field', 'Task type', 'Completion status', 'Project', 'Time period']
  - `VALID Y AXIS (Report on: Task)`: ['Task count', 'Time', 'Time entry', 'Custom field']
  - `VALID X AXIS (Report on: Project)`: ['Project owner', 'Project status', 'Project']
  - `VALID Y AXIS (Report on: Project)`: ['Project count']

## Widget Filters

 1. Task Status Filter
   ```json
  {
    "taskStatus": "Upcoming"
  }
  ```
`Accepted Values`: ['Upcoming', 'Overdue', 'Unscheduled', 'Completed']

2. Task Completion Status Filter
  ```json
  {
    "taskCompletionStatus": "Incomplete"
  }
  ```
`Accepted Values`: ['Completed', 'Incomplete']

3. Date Filter
 ```json
  "date": {
    "dateField": "Due date",
    "type": "Within the last",
    "value": 2,
    "unit": "Weeks"
  }
  ```
Accepted `dateField` values: ['Due date', 'Creation date', 'Completion date']

Accepted `type` values:

 A. `Within the last`
  ```json
 {
  "type": "Within the last",
  "value": 3,
  "unit": "Days" | "Weeks" | "Months"
  }
  ```
 B. `Within the next`
 ```json
{
  "type": "Within the next",
  "value": 2,
  "unit": "Days" | "Weeks" | "Months"
}
```
C. `Between`
```json
{
  "type": "Between",
  "from": "2025-04-01",
  "to": "2025-05-01"
}
```
D. `On`
```json
{
  "type": "On",
  "value": "2025-05-20"
}
```

## Example of body with filters

```json
{
  "name": "This is my Custom Widget",
  "chartDetails": {
    "chartStyle": { "color": "#A69FF3", "type": "Bar" },
    "reportOn": "Tasks",
    "includeTasksFrom": ["My workspace"],
    "showDataLabels": true
  },
  "chartAxes": {
    "xAxis": "Assignee",
    "yAxis": "Task count"
  },
  "filters": {
    // "taskStatus": "Upcoming",
    // "taskCompletionStatus": "Completed",
    "date": {
        "dateField": "Due date",
        "type": "On",
        "value": "2025-05-20"
    }
  }
}
```

## Step 2: Submit the Request
   Response after creating your pre-defined or custom widget.

  ```json
  {
      "success": true,
      "message": "Widget created successfully",
      "data": {
          "id": "147926af-2a3f-45ce-b84d-92bc78d727a7",
          "user_id": "47cba697-d5f5-435c-9a74-95c1d124f71a",
          "name": "My Custom Widget",
          "chart_details": {
              "chartStyle": {
                  "color": "#A69FF3",
                  "type": "Bar"
              },
              "reportOn": "Tasks",
              "includeTasksFrom": [
                  "My workspace"
              ],
              "showDataLabels": true
          },
          "chart_axes": {
              "xAxis": "Creator",
              "yAxis": "Task count"
          }
      }
  }
  ```
