# GitHub Actions Secret Attacker Workflows

**Author:** Carlos Biagolini-Jr.

**LinkedIn:** https://www.linkedin.com/in/biagolini/

**Medium:** https://medium.com/@biagolini

**Companion article:** https://medium.com/@biagolini/41cee1adac12

> **Didactic notice:** This project was developed as a practical example to accompany a blog post. The architecture decisions made here were chosen to meet an educational objective. They illustrate concepts clearly, not necessarily in the most production-ready way. Feel free to draw inspiration from these ideas, but remember to evaluate the limitations and constraints of your own business before adopting any of them. This project is released under the [MIT License](./LICENSE): you are free to copy, modify, and use it as you wish, but it comes with no warranties and the author takes no responsibility for its use in any environment.

## Overview

The attacker-controlled repository for the secret exfiltration defense article. It holds a single reusable workflow, `.github/workflows/leak.yml`, that declares a secret named `target` and prints it. When a service repository calls this workflow and passes a secret to `target`, it runs this external code with that secret, which demonstrates how a pipeline can execute code from another repository and leak a secret that never appears in the service repository itself.

- `.github/workflows/leak.yml` is a reusable workflow (`on: workflow_call`) that receives a `target` secret and runs `echo "${{ secrets.target }}" | base64`. It is the same leak step shown in the article, exposed through `workflow_call` so another repository can invoke it with `uses:`. The caller passes the secret by name (not with `secrets: inherit`, which only works within the same organization).

This repository exists only to illustrate the "run code from another repository" attack described in the article. It performs no action beyond printing an encoded secret to the workflow log.

## License

MIT, see [LICENSE](./LICENSE).
