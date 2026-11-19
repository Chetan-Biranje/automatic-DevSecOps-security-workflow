# DevSecOps security workflow

A GitHub Actions workflow that runs three checks on every push and pull request.
Copy `.github/workflows/security.yml` into another repository to use it.

| Job | Tool | What it catches |
|---|---|---|
| `secrets` | Gitleaks | Keys and tokens committed to the repository, including history |
| `sast` | Semgrep (`p/default`) | Common insecure code patterns |
| `filesystem` | Trivy | Known vulnerable dependencies and misconfigured files (CRITICAL and HIGH only) |

The workflow has read-only permissions, Trivy is pinned to a release instead of
`master`, and each job fails the build when it finds something.

## Notes

* Gitleaks needs a license key for repositories owned by an organization. Personal
  repositories do not.
* Findings you decide to accept can be listed in `.trivyignore`, `.semgrepignore` and
  `.gitleaksignore`.

## History

This repository started as a larger "CyberLab" folder layout (forensics, threat
intel, red team, cloud). Those folders only held empty placeholder files, so they
were removed. The workflow is the part that was working. Related work:
[Secure-CI-CD-pipelines](https://github.com/Chetan-Biranje/Secure-CI-CD-pipelines),
[API authorization scanner](https://github.com/Chetan-Biranje/API-Authorization-Matrix-Automated-BOLA-BFLA-Detection).
