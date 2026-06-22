# Lab — Reset, Amend e Revert

**DevOps I · Aula 12.1 · Unidade 2**

---

## Quando usar cada um

| Comando | Efeito | Use quando |
|---------|--------|------------|
| `git reset --soft HEAD~1` | Desfaz o commit, mantém staged | Comitou cedo demais |
| `git reset HEAD~1` (mixed, padrão) | Desfaz o commit, limpa o stage | Quer revisar antes de comitar de novo |
| `git commit --amend` | Substitui o último commit | Corrigir mensagem/conteúdo, **antes do push** |
| `git revert <hash>` | Cria um novo commit que desfaz outro | O commit **já foi publicado** |

> Regra prática: se ainda não saiu da sua máquina, use `reset`. Se já está no GitHub, use `revert`.

---

## Exercício — A sequência completa

### Passo 1 — Clone e crie sua branch

```bash
git clone git@github.com:alanrpereira88/lab-aula12-reset-revert-amend.git
cd lab-aula12-reset-revert-amend
git switch -c practice/seu-nome
```

### Passo 2 — `reset --soft`

```bash
echo "linha 1 - [seu nome]" >> notas.txt
git add notas.txt
git commit -m "feat: adiciona linha 1"
git reset --soft HEAD~1
git commit -m "feat: adiciona linha 1 do perfil"
```

### Passo 3 — `reset` (mixed)

```bash
echo "linha 2 - [seu nome]" >> notas.txt
git add notas.txt
git reset
git add notas.txt
git commit -m "feat: adiciona linha 2 do perfil"
```

### Passo 4 — `amend`

```bash
echo "linha 3 com erro de digitacao" >> notas.txt
git add notas.txt
git commit -m "feat: adicona linha 3"
# corrija o conteúdo do arquivo
git add notas.txt
git commit --amend -m "feat: adiciona linha 3 do perfil"
```

### Passo 5 — Publique a branch

```bash
git push origin practice/seu-nome
```

### Passo 6 — `revert` em commit já publicado

```bash
echo "linha indesejada" >> notas.txt
git add notas.txt
git commit -m "feat: linha que vou reverter"
git push origin practice/seu-nome

git revert HEAD -m "revert: remove linha indesejada"
git push origin practice/seu-nome
```

---

## Entrega

Sem print, sem e-mail — avaliação direta no histórico da sua branch `practice/seu-nome` no GitHub.

---

## Estrutura do repositório

```
lab-aula12-reset-revert-amend/
├── README.md     ← você está aqui
└── notas.txt     ← arquivo de prática
```
