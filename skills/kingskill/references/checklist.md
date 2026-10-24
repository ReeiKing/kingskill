# Checklist por área

Use o que se aplica à stack do projeto. Cada item é uma pergunta a responder com evidência.

## 1. Construção e configuração
- O projeto compila do zero sem avisos? Quantos avisos, de que tipo?
- Dependências: desatualizadas (`npm outdated`, `swift package show-dependencies`), sem uso, duplicadas, versão travada (lockfile commitado)?
- Versões de linguagem/runtime coerentes (Node, Swift 5 vs 6, TypeScript strict)?
- Scripts de build/deploy reprodutíveis e documentados? Variáveis de ambiente listadas num `.env.example`?
- Tempo de build e tamanho do artefato (bundle JS, .app, imagem Docker).

## 2. Segurança
- Segredos no código ou no histórico do git (`git log -p | grep -iE "key|secret|token|password"`, arquivos `.env` commitados, chaves `service_role` no front-end).
- Vulnerabilidades em dependências (`npm audit --omit=dev`, avisos do GitHub).
- Autenticação e autorização: rotas/API sem verificação, checagem só no cliente, IDs previsíveis acessíveis por qualquer usuário.
- Supabase: RLS ligado em todas as tabelas expostas, políticas corretas, funções `security definer` com `search_path` fixo, advisors de segurança (`get_advisors`) quando houver projeto conectado.
- Entrada do usuário: SQL montado com string, XSS (`dangerouslySetInnerHTML`, HTML sem escapar), upload sem validar tipo/tamanho, redirect aberto.
- Webhooks e pagamentos: assinatura validada (HMAC), idempotência.
- Cabeçalhos e CORS em apps web; cookies `httpOnly`/`secure`.
- Apps nativos: permissões pedidas só quando necessárias, dados sensíveis no Keychain, assinatura de código.
- Rode a skill `security-review` quando houver alterações pendentes.

## 3. Desempenho e agilidade
- Caminho crítico: o que roda a cada requisição, renderização, quadro ou evento de mouse? Meça.
- Front-end: re-render em excesso (estado/observação amplos), listas sem chave estável, trabalho pesado no render, imagens sem otimizar, bundle grande, waterfalls de requisição, falta de cache.
- Back-end/banco: consultas N+1, falta de índice nas colunas filtradas/ordenadas (EXPLAIN), `select *` em tabelas grandes, paginação ausente, conexões.
- Nativo (Swift/AppKit/SwiftUI): trabalho na main thread, redesenho da tela inteira, timers frequentes, observação ampla em SwiftUI, alocações por evento.
- Inicialização: tempo até a primeira tela.

## 4. Qualidade de código e manutenção
- Arquivos ou funções grandes demais, duplicação, código morto, TODOs antigos.
- Tratamento de erros: erros engolidos, mensagens sem contexto, falhas silenciosas.
- Consistência de nomes e padrões com o resto do projeto.
- Tipagem: `any`, force unwrap (`!`), casts inseguros.

## 5. Testes
- Quantos testes, quanto passa, quanto tempo leva? O que crítico está sem teste (pagamento, login, cálculo, permissões)?
- Testes frágeis (dependem de horário, rede, ordem).

## 6. Banco de dados e dados
- Migrations versionadas e aplicáveis do zero? Seeds de exemplo funcionando?
- Tipos de coluna adequados, chaves estrangeiras, `not null`, índices.
- Backups e restauração (quando houver produção).

## 7. Interface, UX e acessibilidade (quando houver tela)
- Responsivo em celular, contraste, foco de teclado, rótulos de acessibilidade.
- Estados de carregando, vazio e erro.
- Textos em português corretos e consistentes.

## 8. Deploy e operação
- Ambientes separados (local/produção), variáveis corretas em cada um.
- Logs e monitoramento de erros.
- Processo de publicação documentado e seguro (sem passos manuais arriscados).
