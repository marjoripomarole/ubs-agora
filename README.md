# UBS Agora — Site de conscientização sobre sífilis

Site estático de conscientização sobre sífilis, sexo seguro e acesso à UBS Vila Nova Galvão, voltado para adolescentes e jovens adultos.

Baseado em dados primários:
- Boletim Epidemiológico SMS-SP 2025 (Covisa)
- Estudo Fiocruz/Cidacs com 15 milhões de registros de nascimentos (The Lancet Regional Health Americas)
- Boletim Saúde da População Negra — Ministério da Saúde
- Código Penal Brasileiro (Arts. 129, 130, 131)

## Stack

- HTML/CSS/JS puros, zero dependências
- Um único arquivo (`index.html`) + imagem de compartilhamento
- Deploy: Cloudflare Pages (recomendado) ou qualquer static host
- Sem cookies, sem tracking, LGPD-friendly

## Estrutura

```
.
├── public/
│   ├── index.html        # Site principal
│   ├── og-image.png      # Preview 1200x630 pra redes sociais
│   ├── _headers          # Headers de segurança (Cloudflare/Netlify)
│   ├── _redirects        # Redirects (trocar domínio quando comprar)
│   ├── robots.txt        # Indexação SEO
│   └── sitemap.xml       # Sitemap
├── wrangler.toml         # Config Cloudflare Pages
├── .gitignore
└── README.md
```

## Deploy (Cloudflare Pages — recomendado)

### 1. Registrar o domínio

Domínios `.com.br` só no Registro.br. Custa ~R$40/ano.

**Sugestões de nome** (evita `ubsagora` que pode soar como oficial da Prefeitura):
- `correpraubs.com.br`
- `sifilistaaqui.com.br`
- `vainaubs.com.br`

Importante: registre em CNPJ de uma ONG/escola parceira se possível, pra não expor CPF no WHOIS público.

### 2. Criar repositório

```bash
# Local
git init
git add .
git commit -m "Initial site"

# GitHub (ou GitLab)
gh repo create ubs-agora --public --source=. --remote=origin --push
```

### 3. Conectar no Cloudflare Pages

1. Login em dash.cloudflare.com
2. Workers & Pages → Create → Pages → Connect to Git
3. Selecionar o repo
4. Build settings:
   - Framework preset: **None**
   - Build command: (vazio)
   - Build output directory: `public`
5. Save and deploy

Em ~30 segundos você tem URL em `ubs-agora.pages.dev`.

### 4. Apontar domínio próprio

1. No Cloudflare Pages → Custom domains → Set up a domain
2. Colocar `SEUDOMINIO.com.br`
3. Cloudflare mostra os nameservers (ex: `tiago.ns.cloudflare.com`, `maria.ns.cloudflare.com`)
4. No Registro.br → seu domínio → DNS → Configurar usando servidores DNS → colar nameservers do Cloudflare
5. Propagação: 5min a 24h

### 5. Ajustar os placeholders

Depois que o domínio funcionar:

- `public/_redirects`: descomentar a linha do redirect www→apex e trocar `SEUDOMINIO`
- `public/robots.txt`: trocar `SEUDOMINIO.com.br`
- `public/sitemap.xml`: trocar `SEUDOMINIO.com.br`
- `public/index.html`: atualizar `og:image` pra URL absoluta (`https://SEUDOMINIO.com.br/og-image.png`)

Commit e push — deploy automático.

### 6. Analytics sem cookies

Cloudflare Pages → Settings → Web Analytics → Enable. Grátis, sem cookies, não precisa de banner de consentimento LGPD.

## Deploy alternativo (Netlify Drop — sem git)

Pra colocar no ar em 30s sem CLI:

1. Acessa [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrasta a pasta `public/` inteira
3. Conta grátis permite renomear subdomínio e apontar domínio próprio

## Checklist pré-lançamento

- [ ] Validar conteúdo clínico com alguém da UBS Vila Nova Galvão
- [ ] Conferir horário e telefone atuais da UBS (2241-7366)
- [ ] Testar preview em WhatsApp (manda pra si mesmo)
- [ ] Testar preview em Instagram/Twitter via [opengraph.xyz](https://www.opengraph.xyz/)
- [ ] Rodar Lighthouse no Chrome DevTools — mirar 95+ em todas as métricas
- [ ] Testar em celular real (iPhone Safari + Android Chrome)
- [ ] Testar modo escuro e preto-e-branco (acessibilidade)
- [ ] Verificar que todos os links `tel:` funcionam no celular
- [ ] Registrar no Google Search Console
- [ ] Submeter sitemap no Search Console

## Checklist de manutenção (a cada 6 meses)

- [ ] Atualizar número estatístico no hero (`4,6x`) com novo Boletim Covisa
- [ ] Confirmar horário e telefone da UBS
- [ ] Revisar recorte racial se sair novo boletim do Ministério
- [ ] Rodar novo Lighthouse
- [ ] Checar se domínio continua renovado

## Conteúdo

O site tem 9 seções:

1. **Hero** — hook do panfleto
2. **3 Passos** — Corre / Testa / Trata
3. **Alerta** — sobre cancro duro
4. **FAQ** — 6 perguntas com accordion
5. **Dados SP** — estatísticas Covisa/SMS
6. **Recorte racial** — dados Fiocruz + quote
7. **Crime** — Código Penal
8. **Direitos** — ECA, sigilo, acesso universal
9. **UBS + Canais** — endereço, 136, 180, 100, 190

## Como atualizar conteúdo

Edita `public/index.html` direto — é HTML simples, sem framework. Commit e push → Cloudflare faz deploy automático.

Lugares comuns pra alterar:
- Endereço/telefone da UBS → buscar `Alpheu Luiz Gasparini`
- Estatística do hero → buscar `4,6`
- Perguntas do FAQ → buscar `faq-item`

## Acessibilidade

- Navegação por teclado (Tab) funciona em todos os elementos
- `aria-expanded` no accordion
- Contraste AA em todos os textos (verificado em WebAIM Contrast Checker)
- `lang="pt-BR"` declarado
- Meta viewport com `user-scalable=no` NÃO aplicado (usuário pode dar zoom)
- Fontes sistêmicas (sem download bloqueante)

## Performance

- Arquivo HTML: ~36KB
- Total (com OG image): ~130KB
- Zero requisições externas (tudo inline/local)
- Zero JavaScript blocking
- Mobile-first, breakpoints em 500/600/640/768

## Licença

Material educativo de interesse público. Uso livre para fins não comerciais, com crédito.

Dados baseados em fontes públicas. Em caso de dúvidas clínicas, sempre procure profissional de saúde.

---

Em caso de problema: abre uma issue no repo ou manda email pra ADRESS.
