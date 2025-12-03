# Changelog

## [2.0.0] - 2025-12-03

### ✨ Melhorias de Segurança

#### Configurações Sensíveis
- ✅ Implementado suporte para variáveis de ambiente com `python-decouple`
- ✅ Criado arquivo `.env.example` com todas as variáveis necessárias
- ✅ Removido `SECRET_KEY` hardcoded do código
- ✅ `DEBUG` e `ALLOWED_HOSTS` agora configuráveis via `.env`
- ✅ Credenciais de email movidas para variáveis de ambiente

#### Estrutura de Arquivos
- ✅ Corrigido `MEDIA_ROOT` (de `simplemooc/media` para `media`)
- ✅ Adicionado `STATIC_ROOT` para produção
- ✅ Estrutura de arquivos de mídia padronizada

### 🚀 Otimizações de Performance

#### Queries de Banco de Dados
- ✅ Implementado `select_related()` e `prefetch_related()` em todas as views
- ✅ Redução de queries N+1 nas seguintes views:
  - `index`: Lista de cursos com enrollments
  - `details`: Detalhes de curso com lessons
  - `announcements`: Curso com anúncios
  - `show_announcement`: Anúncio com comentários e usuários
  - `lessons`: Curso com lessons e materiais
  - `lesson`: Aula com curso e materiais
  - `my_certificates`: Certificados com course e progress

#### Paginação
- ✅ Adicionada paginação na listagem de cursos (12 por página)
- ✅ Adicionada paginação na listagem de anúncios (10 por página)
- ✅ Tratamento de páginas inválidas e vazias

### 🔧 Correções de Código

#### Duplicações Removidas
- ✅ Removido dashboard duplicado do app `accounts`
- ✅ Consolidado dashboard em `cursos.views.dashboard`
- ✅ Atualizado `accounts/urls.py` para usar dashboard correto

#### Validações e Tratamento de Erros
- ✅ Validação de curso com aulas antes de permitir matrícula
- ✅ Mensagens informativas para usuário já matriculado
- ✅ Tratamento de erro no download de certificados
- ✅ Validação de parâmetros no `ProgressManager`
- ✅ Tratamento de exceções no `CertificateManager`
- ✅ Mensagens de erro amigáveis para o usuário

### 🧪 Testes

#### Cobertura de Testes
- ✅ Testes já existentes mantidos (14 testes)
- ✅ Testes de models: Course, Lesson, Enrollment
- ✅ Testes de managers: ProgressManager, CertificateManager
- ✅ Testes de progresso: LessonProgress, CourseProgress
- ✅ Testes de certificados: Certificate
- ✅ Execute com: `python manage.py test cursos.tests`

### 📦 Dependências

#### Novas Dependências
```
python-decouple==3.8  # Gerenciamento de configurações
```

#### Dependências Existentes
- Django==4.1.7
- Pillow==9.5.0
- reportlab==4.0.6
- djangorestframework==3.14.0
- django-extensions==3.2.3
- django-debug-toolbar==4.1.0

### 📝 Documentação

#### Novos Arquivos
- `.env.example`: Template de variáveis de ambiente
- `CHANGELOG.md`: Histórico de mudanças (este arquivo)

### 🔄 Migração

#### Para Atualizar:

1. **Instalar nova dependência:**
   ```bash
   pip install python-decouple==3.8
   ```

2. **Criar arquivo `.env`:**
   ```bash
   copy .env.example .env
   ```

3. **Configurar variáveis:**
   - Edite `.env` com suas credenciais
   - Gere uma nova `SECRET_KEY` para produção
   - Configure email conforme seu provedor

4. **Executar testes:**
   ```bash
   python manage.py test cursos.tests
   ```

5. **Migrar arquivos de mídia (se necessário):**
   ```bash
   move simplemooc\media\* media\
   ```

### ⚠️ Breaking Changes

- **MEDIA_ROOT alterado**: Arquivos de mídia agora em `/media` (raiz) ao invés de `/simplemooc/media`
- **Dashboard accounts removido**: Agora usa `cursos.views.dashboard`
- **Variáveis de ambiente**: Necessário criar arquivo `.env` para configurações

### 🎯 Próximos Passos Recomendados

1. **Cache**: Implementar Redis para cache de queries frequentes
2. **Async**: Migrar views pesadas para async/await
3. **API**: Expandir DRF para API completa
4. **Frontend**: Adicionar Vue.js ou React para interatividade
5. **Notificações**: Sistema de notificações em tempo real
6. **Analytics**: Dashboard de analytics para instrutores
7. **Testes**: Aumentar cobertura para 90%+

---

## [1.0.0] - 2024-XX-XX

### Versão Inicial
- Sistema completo de gerenciamento de cursos
- Rastreamento de progresso
- Geração de certificados em PDF
- Sistema de matrículas
- Anúncios e comentários
