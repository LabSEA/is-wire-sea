# Publicação no PyPI

O pacote Python deste projeto se chama `is-wire-sea` e é publicado automaticamente no PyPI pelo GitHub Actions.

## Como funciona

O workflow está em `.github/workflows/main.yml`. O envio de uma tag no formato `v*.*.*` executa os testes, gera as distribuições e as publica no PyPI.

Antes de publicar, o workflow verifica se a tag corresponde à versão em `pyproject.toml`. Não é necessário criar um GitHub Release manualmente.

## Publicar uma nova versão

Atualize `version` em `pyproject.toml`, por exemplo para `2.0.3`. Revise o `CHANGELOG.md`, execute os testes e envie a branch principal:

```bash
git add pyproject.toml CHANGELOG.md
git commit -m "release: v2.0.3"
git push origin main
```

Em seguida, crie uma tag com a mesma versão:

```bash
git tag v2.0.3
git push origin v2.0.3
```

O GitHub Actions publicará automaticamente a distribuição `is-wire-sea==2.0.3` no PyPI.

## Trusted Publisher

O projeto no PyPI deve ter um Trusted Publisher configurado com:

```text
Owner: LabSEA
Repository name: is-wire-sea
Workflow name: main.yml
Environment name: pypi
```

No GitHub, crie ou configure o ambiente `pypi` em `Settings > Environments`. O workflow usa OIDC, portanto não armazena token permanente do PyPI como secret.

## Atenção

O PyPI não permite substituir arquivos de uma versão já publicada. Para corrigir uma publicação, aumente a versão. A opção `skip-existing: true` evita que uma reexecução falhe quando os mesmos arquivos já estiverem disponíveis; ela não substitui arquivos existentes.
