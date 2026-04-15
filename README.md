# sudo-policy-linter

Flag broad passwordless sudo rules for manual review.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "policy": "%operators ALL=(ALL) NOPASSWD: ALL\n"
}
```

Result:

```json
{
  "findings": [
    {
      "line": 1,
      "issue": "unrestricted-passwordless-command"
    }
  ]
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Not a sudoers parser or security proof. Validate syntax with visudo and review aliases and includes separately.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [package-pin-auditor](https://github.com/sal-s-root/package-pin-auditor), [rotation-size-planner](https://github.com/sal-s-root/rotation-size-planner).
