# VectorCraft — funcionalidades e módulos

Última atualização: 2026-10-28.

## Fluxo principal

| Etapa | Entradas | Responsabilidade e dependências | Saídas |
|---|---|---|---|
| Abrir e editar | Arquivos vetoriais, objetos e gestos de ferramentas | [doc](../../crates/doc/), [svg](../../crates/svg/), [pathops](../../crates/pathops/), [tools](../../crates/tools/), [engine](../../crates/engine/) | Documento vetorial e histórico de alterações |
| Avaliar e produzir saída | Estado editado e parâmetros de saída | [text](../../crates/text/), [effects](../../crates/effects/), [render](../../crates/render/), [pdf](../../crates/pdf/), [format](../../crates/format/) | Canvas rasterizado e arquivos vetoriais/PDF |
| Acesso pelo usuário ou agente | Gestos, argumentos CLI ou chamadas estruturadas | [apps](../../apps/), [engine](../../crates/engine/) e interfaces descritas abaixo | Estado atualizado, resposta ou erro; comportamento detalhado nos contratos |

A tabela mostra o caminho conceitual, não uma garantia de suporte a todos os formatos. APIs, estruturas, unidades, efeitos colaterais e limites ficam na [arquitetura](../architecture.md), nos documentos de assunto e nos módulos indicados.

## Contratos e exemplos de uso

- [development.md](../development.md)
- [type-parity.md](../type-parity.md)
- [effects-parity.md](../effects-parity.md)
- [three-d.md](../three-d.md)
- [plugins.md](../plugins.md)
- [control-protocol.md](../control-protocol.md)
- [mcp.md](../mcp.md)

## Inventário de bibliotecas

Responsabilidades resumidas a partir dos manifestos e comentários de módulo do checkout. As dependências listadas são as internas diretas declaradas em `dependencies` (incluindo condicionais); não incluem dependências de teste/build nem expansão de features. O manifesto de cada linha é a fonte exata.

| Módulo / manifesto | Responsabilidade declarada | Dependências internas diretas |
|---|---|---|
| [affinity](../../crates/affinity/Cargo.toml) | Bounded reader for native Affinity documents: archive, object stream and document model | Nenhuma declarada nesta categoria |
| [brush](../../crates/brush/Cargo.toml) | VectorCraft brushes: calligraphic, scatter, art, pattern and bristle brush definitions and stroke geometry | `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-geom` |
| [cad](../../crates/cad/Cargo.toml) | VectorCraft CAD interchange: a hand-written ASCII DXF writer (R12 to 2018) | `vectorcraft-brush`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-pathops`, `vectorcraft-text` |
| [color](../../crates/color/Cargo.toml) | VectorCraft color | Nenhuma declarada nesta categoria |
| [doc](../../crates/doc/Cargo.toml) | VectorCraft document model: artboards, layers, objects, appearance (pure data + serde) | `vectorcraft-color`, `vectorcraft-geom` |
| [effects](../../crates/effects/Cargo.toml) | VectorCraft live effects evaluated to geometry | `vectorcraft-doc`, `vectorcraft-geom`, `vectorcraft-pathops`, `vectorcraft-plugins`, `vectorcraft-text`, `vectorcraft-three-d` |
| [engine](../../crates/engine/Cargo.toml) | VectorCraft engine: sessions, history, selection, the command registry | `vectorcraft-affinity`, `vectorcraft-brush`, `vectorcraft-cad`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-eps`, `vectorcraft-format`, `vectorcraft-geom`, `vectorcraft-metafile`, `vectorcraft-pathops`, `vectorcraft-pdf`, `vectorcraft-plugins`, `vectorcraft-render`, `vectorcraft-scriptcheck`, `vectorcraft-svg`, `vectorcraft-text`, `vectorcraft-tools`, `vectorcraft-trace` |
| [eps](../../crates/eps/Cargo.toml) | VectorCraft Encapsulated PostScript: a hand-written EPS writer (PostScript Level 2 and 3) with TIFF previews | `vectorcraft-brush`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-metafile`, `vectorcraft-pdf`, `vectorcraft-render`, `vectorcraft-text` |
| [format](../../crates/format/Cargo.toml) | VectorCraft native .vectorcraft format (versioned JSON, embedded images) | `vectorcraft-doc` |
| [geom](../../crates/geom/Cargo.toml) | VectorCraft geom | Nenhuma declarada nesta categoria |
| [mcp](../../crates/mcp/Cargo.toml) | VectorCraft MCP server: JSON-RPC 2.0 over stdio, driving a running app or a headless session | `vectorcraft-doc`, `vectorcraft-engine`, `vectorcraft-format`, `vectorcraft-geom`, `vectorcraft-render`, `vectorcraft-svg`, `vectorcraft-tools` |
| [metafile](../../crates/metafile/Cargo.toml) | VectorCraft Windows metafiles: hand-written EMF and WMF writers and readers | `vectorcraft-brush`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-text` |
| [pathops](../../crates/pathops/Cargo.toml) | VectorCraft path operations: booleans (Pathfinder), shape builder regions, offset, outline stroke, simplify | `vectorcraft-geom` |
| [pdf](../../crates/pdf/Cargo.toml) | VectorCraft PDF export and import | `vectorcraft-brush`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-text` |
| [plugins](../../crates/plugins/Cargo.toml) | Sandboxed WebAssembly plug-ins for VectorCraft: a resource-limited wasmi host for object filters and live effects | `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-geom` |
| [render](../../crates/render/Cargo.toml) | VectorCraft renderer: document to pixels (vello_cpu backend) | `vectorcraft-brush`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-text` |
| [scriptcheck](../../crates/scriptcheck/Cargo.toml) | Static checker for scripts written for the reference app: what a script uses, without running it | Nenhuma declarada nesta categoria |
| [svg](../../crates/svg/Cargo.toml) | VectorCraft SVG import and export | `vectorcraft-brush`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-text` |
| [testkit](../../crates/testkit/Cargo.toml) | VectorCraft test helpers: fixtures, generators, render comparison, geometry assertions | `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-engine`, `vectorcraft-format`, `vectorcraft-geom`, `vectorcraft-render`, `vectorcraft-svg` |
| [text](../../crates/text/Cargo.toml) | VectorCraft text: font database, shaping, layout, glyph outlines | `vectorcraft-doc`, `vectorcraft-geom` |
| [three-d](../../crates/three-d/Cargo.toml) | Portable 3D effect geometry (revolve, extrude and bevel, inflate, rotate) and projected vector shading | `vectorcraft-geom`, `vectorcraft-pathops` |
| [tools](../../crates/tools/Cargo.toml) | VectorCraft tool state machines: pointer events in, commands and overlays out | `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-geom`, `vectorcraft-pathops`, `vectorcraft-text` |
| [trace](../../crates/trace/Cargo.toml) | VectorCraft Image Trace: raster to vector tracing (quantize, boundary follow, polygon, Bezier fit) | `vectorcraft-geom` |
| [ui-egui](../../crates/ui-egui/Cargo.toml) | VectorCraft egui frontend (menus, panels, tools and canvas); swappable — nothing below depends on it | `vectorcraft-brush`, `vectorcraft-cad`, `vectorcraft-color`, `vectorcraft-doc`, `vectorcraft-effects`, `vectorcraft-engine`, `vectorcraft-eps`, `vectorcraft-format`, `vectorcraft-geom`, `vectorcraft-pdf`, `vectorcraft-plugins`, `vectorcraft-render`, `vectorcraft-svg`, `vectorcraft-text`, `vectorcraft-three-d`, `vectorcraft-tools` |

Ao mudar uma entrada, saída ou dependência, atualize primeiro o contrato do módulo e depois esta navegação. [Voltar ao índice](../INDEX.md).
