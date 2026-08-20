# React Test Quality

**[Instalar com skills.sh](https://skills.sh/thiagocrepequer/react-test-quality/react-test-quality)**

```bash
npx skills add ThiagoCrepequer/react-test-quality
```

Skill para agentes de código projetarem, escreverem e revisarem testes confiáveis em React e JavaScript/TypeScript.

## O que ela faz

Orienta o agente a transformar fluxos do usuário e contratos públicos em evidências executáveis. A skill cobre Testing Library, Vitest/Jest, interações reais, acessibilidade, rede, formulários, stores, caches, roteamento, concorrência assíncrona, testes de navegador e StrykerJS.

Ela ajuda a evitar testes que passam sem provar a experiência, como verificar apenas que um elemento existe, mockar hooks e clientes essenciais, depender de snapshots amplos, compartilhar estado entre cenários ou mostrar sucesso sem validar requisição e resposta.

## Filosofia

Um bom teste deve ser simultaneamente:

- **sensível a regressões:** uma quebra plausível no comportamento faz o teste falhar;
- **tolerante a refatorações:** componentes, hooks e estado podem mudar internamente sem quebrar o contrato;
- **centrado no usuário:** interage e observa pela superfície pública e acessível;
- **isolado e determinístico:** cada teste recebe stores, caches, handlers, timers e dados novos;
- **honesto:** distingue evidência de componente, rede e navegador e explicita o que não foi provado.

Mutation score e cobertura são sinais de diagnóstico. A confiança vem de estados significativos, interações fiéis e um oráculo independente capaz de detectar resultados incorretos, efeitos proibidos e condições de corrida.

## Conteúdo

O entrypoint está em [`react-test-quality/SKILL.md`](react-test-quality/SKILL.md). As referências aprofundam princípios de bons testes, camadas frontend, asserções semânticas, fixtures, test doubles, isolamento assíncrono e análise de mutações.

## Uso

```text
$react-test-quality Escreva testes para este formulário e prove payload, resultado visível e ausência de submissão duplicada.
```

Licenciado sob [MIT](LICENSE).
