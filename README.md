# sdlc-developer-agent

Agente `developer` do [agentic-sdlc-reference-architecture](https://github.com/leandrosflora/agentic-sdlc-reference-architecture) — implementação operacional do papel `agent_role == "developer"` definido em `policies/agent_authorization.rego`.

## Responsabilidade

Único papel autorizado a escrever código de aplicação, sempre em branch e nunca em branch protegida; dono do **Build gate** (diff dentro do escopo, commit assinado, licenças permitidas e SBOM).

## Autorização (OPA)

- `project.read`: permitido, restrito ao próprio `project_id`.
- `repository.write`: permitido apenas quando `resource.protected_branch` é falso, `change.risk` está em `{R1, R2}` e `change.scope_approved` é verdadeiro.
- `architecture.propose`: permitido, restrito ao próprio `project_id` e a `change.risk` em `{R0, R1}` — proposta apenas; escrita direta é exclusiva do papel `architecture` (`architecture.update`).
- Sem permissão para acionar deploy ou alterar arquitetura/contratos diretamente.

## Status

Scaffold inicial (Python/.pyproj). Lógica do agente ainda não implementada.

## Referências

- Governança e gates: [docs/governance.md](https://github.com/leandrosflora/agentic-sdlc-reference-architecture/blob/main/docs/governance.md)
- Política: [policies/agent_authorization.rego](https://github.com/leandrosflora/agentic-sdlc-reference-architecture/blob/main/policies/agent_authorization.rego)
