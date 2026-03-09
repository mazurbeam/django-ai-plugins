# CDRF Expert Plugin

A Django REST Framework skill focused on Classy DRF (https://www.cdrf.co) to select the right class-based views and override points with confidence.

## What this skill covers

- Selecting the right DRF class (`APIView`, generic views, `ViewSet`, `ModelViewSet`)
- Tracing class behavior with CDRF MRO and method source mapping
- Choosing safe override hooks (`perform_*`, `get_queryset`, `get_serializer_class`)
- Handling DRF version-specific behavior differences

## Plugin structure

```
cdrf-expert/
├── .claude-plugin/plugin.json
├── skills/SKILL.md
└── skills/references/
    ├── class-selection-matrix.md
    ├── lifecycle-and-overrides.md
    ├── mro-debugging-playbook.md
    └── version-check-workflow.md
```
