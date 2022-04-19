# In this repo
This is a template for a ROS2 package.

# Pre-commit
The project uses [pre-commit](https://pre-commit.com/) to enforce code styles.
To run the pre-commit, run
```bash
pre-commit run -a
```
To set pre-commit as a commit hook, then install pre-commit in the repo using
```bash
pre-commit install
```
To update the `.pre-commit-config.yaml` file:
```bash
pre-commit autoupdate
```