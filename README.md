# Composer install with local cache
This action is useful if you are using **self hosted Github runners** on your own hardware. We found that the standard [github/cache](https://github.com/actions/cache) used in combination with composer was to slow. It's much faster to use a common volume (we use a docker volume) and store the composer cache there. This actions does exactly that.

This action uses **zstd compression** for faster compression/decompression speeds and better compression ratios compared to traditional gzip.

### Usage
```
      - uses: Vendic/composer-install-with-local-cache-action@master
        name: Cached composer install
        with:
          composer_install_options: --prefer-dist --no-interaction
          cache_dir: /home/composer-cache/vendor
          zstd_compression_level: 1  # Optional: 1-19 (1=fastest, 19=best compression)
```

**Note:** This action requires `zstd` to be installed on your runner.

