# Bitbucket Pipelines Pipe: CodeScanCloud Quality Gate check

Check the Quality Gate of your code with [CodeScanCloud](https://app.codescan.io) to ensure good quality before releasing or deploying new features.

## YAML Definition

Add the following snippet to the script section of your `bitbucket-pipelines.yml` file:

```yaml
- pipe: codescan/codescancloud-quality-gate:0.1.0
  # variables:
  #   SONAR_QUALITY_GATE_TIMEOUT: '<int>'  # Optional
```

## Variables

| Variable           | Usage                                                       |
| --------------------- | ----------------------------------------------------------- |
| SONAR_TOKEN (*) | CodeScanCloud token. It is recommended to use a secure repository or account variable. And in this case there is no need to specify this variable in the `bitbucket-pipelines.yml` file. |
| SONAR_QUALITY_GATE_TIMEOUT | Maximum seconds to wait to get quality gate status. Default value is 300 (5 minutes). |

_(*) = required variable._

## Details

This pipe takes the task id from the report produced by the [CodeScanCloud Scan pipe][codescancloud-scan-pipe]
and polls CodeScanCloud until the quality gate result is ready.

If the quality gate passes, the pipe completes with success.

If the quality gate fails, the pipe prints the failed conditions and exits with failure.

## Prerequisites

To use this pipe you must have the [CodeScanCloud Scan pipe][codescancloud-scan-pipe] earlier in the pipeline.

## Examples

Basic example:

```yaml
- pipe: codescan/codescancloud-quality-gate:0.1.0
```

A bit more advanced example:

```yaml
- pipe: codescan/codescancloud-quality-gate:0.1.0
  variables:
    SONAR_QUALITY_GATE_TIMEOUT: 180  # 3 minutes
```

## Support

If you would like help with this pipe, or you have an issue or feature request, [let us know on our support email][mailto:support@code-scan.com].

If you are reporting an issue, please include:

* the version of the pipe
* relevant logs and error messages
* steps to reproduce

[codescancloud-scan-pipe]: https://github.com/VillageChief/codescancloud-scan/src/master/README.md

