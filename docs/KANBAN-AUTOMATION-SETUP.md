# KANBAN Automation Setup

## Introduction
This document provides detailed instructions for setting up automation for your GitHub Projects Kanban board, including column automation setup for the key stages: **To Do**, **In Progress**, **QA/Testing**, and **Done**. 

## Prerequisites
- A GitHub repository with GitHub Projects enabled.
- Access to the repository where you want to set up the Kanban board.

## Creating the Kanban Board
1. Navigate to the `Projects` tab in your repository.
2. Click on `New Project`.
3. Select `Kanban` template or `Create from template` if you have predefined columns.
4. Name your project (e.g., `Project Kanban`) and configure it as per your needs.

## Setting Up Columns
To create the required columns for your workflow:
- **To Do**: This is where all new tasks will be added.
- **In Progress**: This column will contain tasks that are currently being worked on.
- **QA/Testing**: Use this column for tasks that are under review or testing.
- **Done**: Completed tasks will move to this column.

### Adding Columns
1. Click on `Add Column` in your Kanban board.
2. Enter the name of the column (e.g., `In Progress`).
3. Repeat for `QA/Testing` and `Done`.

## Automation Setup
### Column Automation
1. Go to the *three dots* (⋮) on the column header for each stage you want to automate.
2. **For `To Do`**: Set rules to move cards automatically when they are tagged with certain labels (such as `ready for development`).
3. **For `In Progress`**: Automatically move cards to `In Progress` when they are assigned to a user.
4. **For `QA/Testing`**: Move cards to this column once a pull request has been created.
5. **For `Done`**: Configure this column to accept cards that are linked to closed pull requests.

### Example Automation Rules
- Automatically move items to **In Progress** when assigned
- Automatically move items to **QA/Testing** when a label like `in review` is added
- Automatically move items to **Done** when a pull request is merged.

## GitHub Actions Integration
To enhance automation with GitHub Actions:
1. Create a `.github/workflows/kanban.yml` file in your repository.
2. Define workflows that listen to pull request events and update board columns accordingly.

### Sample Workflow
```yaml
name: Update Kanban Board

on:
  pull_request:
    types: [closed]

jobs:
  move-card:
    runs-on: ubuntu-latest
    steps:
    - name: Move Card to Done
      uses: actions/github-script@v4
      with:
        script: |
          // Use GitHub API calls to update project cards status
```

## Status Tracking Guidance
- Utilize the Kanban board to visually track the status of each task.
- Encourage team members to update the status of their tasks regularly.
- Use the `Projects` tab to filter through tasks based on their current status.

## Conclusion
Following this guide will help you establish a well-structured Kanban board with automation tailored to streamline your development workflow. Regularly reviewing and updating your board is key to maintaining efficient project management.