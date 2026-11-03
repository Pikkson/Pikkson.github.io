# Lever Torque Calculator

A standalone, dependency-free HTML calculator for estimating the static torque required to hold a horizontal lever and the additional payload it can support.

## Run locally

Open `index.html` in any modern browser. No build step, server, package installation, or internet connection is required.

## Publish with GitLab Pages

1. Add `index.html` to the root of your GitLab repository.
2. Add the following `.gitlab-ci.yml` file:

```yaml
pages:
  stage: deploy
  script:
    - mkdir -p public
    - cp index.html public/
  artifacts:
    paths:
      - public
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

3. Commit and push. GitLab Pages will publish the calculator when the pipeline succeeds. Enable Pages for the project if prompted.

## Calculation

For a horizontal arm with a payload at its tip and a uniformly distributed arm mass:

`required torque = g * (payload mass * arm length + arm mass * arm length / 2)`

The maximum payload is calculated using the selected usable fraction of the motor's stall torque, less the torque required to support the arm itself.

## Assumptions and limitations

- Static loading, with the arm held horizontally.
- Payload is concentrated at the arm tip.
- Arm mass is uniformly distributed, so its centre of mass is at half its length.
- Gravity is fixed at 9.81 m/s².
- Excludes friction, acceleration, impacts, gearbox losses, compliance, and speed/voltage effects.
- Stall torque is not a continuous operating rating. Confirm continuous and dynamic motor limits in the manufacturer's documentation and apply an appropriate safety factor before using the result for a physical design.

This tool is an engineering estimate, not a safety certification.
