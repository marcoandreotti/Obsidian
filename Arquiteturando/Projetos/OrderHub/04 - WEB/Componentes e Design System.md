# Componentes e Design System

Fonte oficial: `docs/web-design-system.md`; tokens `web/OrderHub.Web/src/themes/_tokens.scss`, tema/appearance e `src/css/app.scss`.

Compartilhados atuais: `src/components/ProblemBanner.vue` (erros recuperáveis) e `AppearanceControl.vue` (preferência Sistema/Claro/Escuro). Componentes de feature permanecem junto ao domínio: PublicUnitContext/Search/CategoryNavigation/ProductCard/CartAccess; catalog picker/tables/grid; OperationsOrderCard/SyncStatus; KitchenColumn/TicketCard.

O catálogo oficial não lista `AppButton`, `AppCard`, `AppDialog`, `AppStatus`, `AppPageHeader`. Classifique novo componente Global/Domain-Feature/Page-specific; não crie wrapper que só repasse props e não promova componente de feature sem reuso comprovado.

Superfícies diferentes: Public mobile-first e tema Tenant; Administration produtividade; Operations rapidez/estado; KDS leitura à distância; Platform contexto global. Tokens têm primary `#F97316`, neutros, status e accent administrativo. Tema Tenant somente no subtree Public; claro/escuro usa tokens semânticos.

Considere estados assíncronos, teclado/foco, labels/semântica, contraste e touch. Estado não pode ser comunicado só por cor. Specs `openspec/specs/web/action-controls/spec.md`, `openspec/specs/web/appearance-preferences/spec.md`; consulte código/tokens antes de alterar.




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

