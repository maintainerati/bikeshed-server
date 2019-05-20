Maintainerati Bikeshed Server
=============================

## Requirements

  - PHP 7.2+
  - Composer 1.5+

### Development

  - Yarn

## Installation

```bash
composer create-project maintainerati/bikeshed-server my-bikeshed-server
```

## Set-up

#### `config/routes.yaml`

```yaml
bikeshed:
    resource: .
    type: bikeshed
```

#### `config/packages/api_platform.yaml`

```yaml
api_platform:
    mapping:
        paths:
            - '%kernel.project_dir%/vendor/maintainerati/bikeshed/src/Entity'
```

#### `config/packages/assets.yaml`

```yaml
framework:
    assets:
        json_manifest_path: '%kernel.project_dir%/public/assets/manifest.json'
        packages:
            assets:
                base_path: 'assets'
            images:
                base_path: 'assets/images'
```

#### `config/packages/knp_menu.yaml`

```yaml
knp_menu:
    twig:
        template: '@Bikeshed/_partials/menu.html.twig'
    templating: false
    default_renderer: twig
```

#### `config/packages/security.yaml`

```yaml
security:
        bikeshed:
            anonymous: true
            guard:
                authenticators:
                    - Maintainerati\Bikeshed\Security\FormAuthenticator
                entry_point: Maintainerati\Bikeshed\Security\FormAuthenticator
                provider: bikeshed_user_provider
            remember_me:
                name: maintainerati
                secret:   '%kernel.secret%'
                lifetime: 604800
                secure: true
                remember_me_parameter: remember
            logout:
                path:   bikeshed_logout
```

#### `config/packages/twig.yaml`

```yaml
twig:
    form_themes:
        - '_form/form_layout.html.twig'
    globals:
        site_name: Maintainerati Bikeshed
        site_tagline: ~
```

#### `config/packages/webpack_encore.yaml`

```yaml
webpack_encore:
    output_path: '%kernel.project_dir%/public/assets'
```
