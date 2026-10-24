# Homies

ASP.NET Core (.NET 6) application with NUnit unit and integration tests.

## CI/CD

- **GitHub Actions** – `.github/workflows/ci.yml` restores, builds and runs all tests on every push to `develop` and `feature/**` branches.
- **Jenkins** – `Jenkinsfile` restores, builds and runs all tests whenever changes are pushed to `main`.
