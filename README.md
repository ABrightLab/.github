# Code movement process

## Environments

- Development (dev)
- Quality Assurance (qa)
- Pre-Production (pre-prod)
- Production (prod)

## Branch Structure

- `main` - Production code
- `staging` - Pre-production code
- `release/*` - QA testing code
- `dev` - Development integration
- `feature/*` - Feature branches
- `hotfix/*` - Emergency fixes

## Workflow

### Feature Development

1. Create feature branch from `dev`
   ```bash
   git checkout develop
   git checkout -b feature/new-feature
   ```
2. Develop and commit changes
3. Submit PR to `dev`
4. After review, merge to `dev`

### Environment Promotion

1. **Dev → QA**

   ```bash
   git checkout release/*
   git merge develop
   git push origin release/*
   ```

2. **QA → Pre-prod**

   ```bash
   git checkout staging
   git merge release/*
   git push origin staging
   ```

3. **Pre-prod → Prod**
   ```bash
   git checkout main
   git merge staging
   git tag v1.x.x
   git push origin main --tags
   ```

### Hotfixes

1. Branch from `main`
   ```bash
   git checkout -b hotfix/critical-fix main
   ```
2. Fix and test
3. Merge to `main` and backport to all environments
4. Tag new version

## Release Process

1. Create release branch from `develop`
2. Test and stabilize
3. Merge to environments sequentially
4. Tag final release in `main`
