# first-gilab-ci-pipeline
# CI/CD Pipeline Description — *My Awesome App Pipeline*

This GitLab CI/CD configuration defines a simple pipeline with **one job** that runs on the **`test`** stage and is triggered **only for commits to the `main` branch**.

---

## When it runs
- **Rule:** `if: '$CI_COMMIT_BRANCH == "main"'`  
  The pipeline executes **only** when the commit is pushed to the `main` branch. Pushes to other branches will **not** start this pipeline.

---

## Pipeline stages
1. `test`  
2. `deploy` *(declared for future use, no jobs yet)*

> The current pipeline stops after the `test` stage because there are no jobs in `deploy`.

---

## Jobs

### `unit_test_job` (stage: `test`)
- **Runner selection:**  
  - Uses runners tagged **`saas-linux-small-amd64`** (typically GitLab SaaS shared runners on Linux/AMD64).  
  - Ensure your project has a runner with this tag available; otherwise, adjust the tag.

- **before_script:**  
  - `echo "Setting up environment for unit tests"`  
    Prints a setup message (placeholder for real setup such as `npm ci`, env variables, etc.).

- **script steps:**
  1. `echo "Running unit tests"` – logs an informational message.
  2. `echo npm test`  
  3. `echo npm test` *(intentional duplicate)*

  > **Note:** The job currently **echoes** `npm test` instead of executing it. Replace with actual commands when ready:
  >
  > ```yaml
  > before_script:
  >   - npm ci
  > script:
  >   - npm test
  > ```

---

## Summary
- **Purpose:** Provide a scaffolded pipeline that runs a test job on `main`.  
- **Next steps:**  
  - Swap `echo npm test` for real test commands.  
  - Add deployment jobs under the `deploy` stage (e.g., `deploy_to_prod`) with appropriate `environment` and `only/except` (or `rules`) settings.  
  - Optionally add caching for Node.js (e.g., `cache: paths: - node_modules/`) to speed up builds.

---
