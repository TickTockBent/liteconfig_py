# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.0] - 2026-03-30

### Changed
- **Breaking:** Double underscore (`__`) in environment variables now produces a literal underscore in the config key instead of a dot. Single underscore (`_`) remains the nesting separator. E.g. `MY__KEY` -> `my_key`, `DATABASE_HOST` -> `database.host`.
- **Breaking:** Without `env_prefix`, only environment variables matching keys that already exist in the loaded config are applied. This prevents system variables (`PATH`, `HOME`, etc.) from polluting the config tree. Set `env_prefix` to allow creating new keys from env vars.
- **Breaking:** `__getitem__` (`config['key']`) now returns `None` for keys that exist with a `None` value, instead of raising `KeyError`. `KeyError` is only raised for truly missing keys.
- Replaced unmaintained `toml` package with stdlib `tomllib` (Python 3.11+) / `tomli` (Python 3.8-3.10).
- `.env` file loading now uses `python-dotenv` when installed (supports multiline values, variable interpolation, `export` prefixes), falling back to the built-in parser.

### Added
- `python-dotenv` as an optional dependency (`pip install liteconfig_py[dotenv]`).
- `tomli` as an optional dependency for TOML support on Python < 3.11 (`pip install liteconfig_py[toml]`).

### Fixed
- Environment variable override no longer injects all system env vars when no prefix is set (#4).
- `config['key']` no longer raises `KeyError` for keys with `None` values (#2).
- Double underscores in env var names are now distinguishable from single underscores (#1).

## [0.2.0] - 2025-10-23

### Added
- Native .env file loading functionality with `load_dotenv` parameter
- Pydantic schema validation support with `validate()` and `validate_section()` methods
- Comprehensive type hints throughout the codebase
- Full PEP 561 compliance with `py.typed` marker file
- Code coverage reporting with Codecov integration
- Five production-ready examples:
  - `validation_example.py` - Schema validation with Pydantic
  - `multi_env_example.py` - Multi-environment configuration management
  - `production_setup.py` - Production deployment guide
  - `dotenv_example.py` - Comprehensive .env file usage
  - `basic_usage.py` - Enhanced basic usage examples
- Comprehensive examples documentation (353 lines)
- GitHub Actions CI/CD workflow:
  - Multi-platform testing (Ubuntu, Windows, macOS)
  - Multi-version testing (Python 3.8, 3.9, 3.10, 3.11, 3.12)
  - Automated linting with flake8
  - Type checking with mypy
  - Code coverage reporting
- Professional README badges (CI, coverage, PyPI, license, code style)
- Extensive test suite with 48 tests covering:
  - Core configuration loading (30 tests)
  - Pydantic validation (13 tests)
  - .env file loading (6 tests)
- Support for quoted values in .env files
- Support for comments and empty lines in .env files
- Preservation of existing environment variables (no override from .env)

### Changed
- Minimum Python version updated to 3.8+ (from 3.6+)
- Enhanced error messages for better debugging
- Improved documentation with usage patterns and best practices
- Updated package metadata and author information

### Improved
- Test coverage increased to 95%+
- Documentation expanded with security best practices
- Examples now include production-ready patterns
- Better handling of edge cases in configuration loading

## [0.1.0] - 2025-10-23

### Added
- Initial release of liteconfig_py
- Multi-format configuration support:
  - JSON (built-in)
  - YAML (optional dependency: PyYAML)
  - TOML (optional dependency: toml)
- Environment variable override functionality
- Dot notation for nested configuration access
- Dictionary-style configuration access with `[]` operator
- Optional environment variable prefix filtering
- Comprehensive test suite with 13 initial tests
- MIT License
- Complete README documentation with examples
- Basic usage example script

### Features
- Zero dependencies for core functionality
- Automatic type conversion from environment variables
- Support for nested configuration structures
- Default value support for missing keys
- Clean and intuitive API

[0.3.0]: https://github.com/TickTockBent/liteconfig_py/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/TickTockBent/liteconfig_py/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/TickTockBent/liteconfig_py/releases/tag/v0.1.0
