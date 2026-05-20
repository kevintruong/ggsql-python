# Changelog

## UNRELEASED

### Changed

- `VegaLiteWriter.render_chart()` and `render_altair()` now accept `validate`, `height`, and `width` as explicit keyword arguments. `height` and `width` default to `None`, which preserves whatever dimensions ggsql produces. `validate` defaults to `False` (same behavior as before, now a named parameter).

## 0.3.2

### Changed

- Upgraded to ggsql Rust crate v0.3.2.
- `render_altair()` and `VegaLiteWriter.render_chart()` now default to `validate=False` when creating Altair chart objects. This avoids `ValidationError`s for valid specs (e.g., boxplots) that use Vega-Lite features not yet reflected in Altair's schema. Pass `validate=True` to re-enable.
- When Altair can't deserialize a spec into the expected chart subclass (e.g., `LayerChart`), the converter now falls back to `altair.Chart` instead of raising. The chart still displays correctly; only Altair-level round-tripping (`.to_dict()`) is lost.

## 0.3.1

### Changed

- Upgraded to ggsql Rust crate v0.3.1.
- Replaced polars with Arrow (via pyarrow) for the Rust↔Python data bridge. `DuckDBReader.execute_sql()`, `Spec.data()`, `Spec.layer_data()`, and `Spec.stat_data()` now return `pyarrow.Table` instead of `polars.DataFrame`. `DuckDBReader.register()` accepts `pyarrow.Table` (polars DataFrames are still accepted via automatic conversion). Custom readers returning polars DataFrames from `execute_sql()` continue to work without changes.
- Runtime dependency changed from `polars` to `pyarrow`.

## 0.2.7

Synced with ggsql Rust crate v0.2.7.

## 0.1.4

Initial release.
