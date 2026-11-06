# Composer install with GitHub Actions cache
This action provides fast composer install with caching using GitHub Actions cache. It uses **zstd compression** for faster compression/decompression speeds and better compression ratios compared to traditional gzip, while leveraging GitHub's built-in cache infrastructure.

This action works with both self-hosted and GitHub-hosted runners, providing efficient caching without requiring local disk storage management.

### Usage
```yaml
      - uses: Vendic/composer-install-with-local-cache-action@master
        name: Cached composer install
        with:
          composer_install_options: --prefer-dist --no-interaction  # Optional
          cache_prefix: composer-vendor  # Optional: cache key prefix
          zstd_compression_level: 1  # Optional: 1-19 (1=fastest, 19=best compression)
```

### Outputs
- `cache_key`: The cache key used for caching
- `cache_hit`: Whether the cache was hit (`true`) or missed (`false`)

On a vendor cache miss, the action also restores Composer's downloaded package archives from the newest cache entry, so a changed `composer.lock` only downloads the packages that changed. The action sets `COMPOSER_CACHE_DIR` to `$RUNNER_TEMP/composer-cache` for the rest of the job.

**Note:** This action requires `zstd` to be installed on your runner.

