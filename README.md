# SBOM Deployment Workflows

This repository includes two GitHub Actions to handle SBOM (Software Bill of Materials) management for multiple Apache Maven-related projects.
These workflows automate the process of generating and/or fetching SBOMs and uploading them to DependencyTrack for continuous vulnerability tracking.

## Workflows

### 1. `build-upload-sboms.yml`

This workflow:
- Clones each repository listed in `repos.json`
- Builds it locally using Maven
- Generates an SBOM using the [CycloneDX Maven plugin](https://github.com/CycloneDX/cyclonedx-maven-plugin)
- Uploads the generated SBOM to DependencyTrack

> Use this when you want SBOMs built from source.

### 2. `fetch-upload-sboms.yml`

This workflow:
- Fetches published artifact metadata from Maven Central
- Downloads any available pre-generated CycloneDX JSON SBOMs
- Uploads them to DependencyTrack

> Use this when SBOMs are already published to Maven Central.

---

## Repository List Configuration

The list of repositories is maintained in the `repos.json` file. Each entry must include:

- `name`: Unique display name used for DependencyTrack
- `url`: Git repository URL (used only by the `build-upload-sboms.yml` workflow)
- `groupId`: Maven group ID (used to construct the Maven Central path)
- `artifactId`: Maven artifact ID

### Example `repos.json` entry:

```json
{
  "name": "maven-dependency-plugin",
  "url": "https://github.com/apache/maven-dependency-plugin.git",
  "groupId": "org.apache.maven.plugins",
  "artifactId": "maven-dependency-plugin"
}
