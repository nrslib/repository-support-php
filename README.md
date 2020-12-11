# Repository Support
Support creating repository by file.

# Sample

## Repository
```php
interface UserRepositoryInterface
{
    function find(UserId $id): ?User;

    function save(User $user): void;
}
```

```php
use nrslib\RepositorySupport\FileRepository;

class FileUserRepository implements UserRepositoryInterface
{
    use FileRepository;

    function find(UserId $id): ?User
    {
        $user = $this->load($id->getValue());
        if (is_null($user)) {
            return null;
        } else {
            return $user;
        }
    }
    
    public function save(User $user): void
    {
        $id = $user->getId()->getValue();
        $this->store($id, $user);
    }
}
```

## Setup
### in Laravel
```php
use nrslib\RepositorySupport\FileRepositoryConfig;

class AppServiceProvider extends ServiceProvider
{
    ...
    
    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        // set directory here
        $debugPersistenceDirectoryFullPath = storage_path("debug\\persistence");
        FileRepositoryConfig::$basicDirectoryFullPath = $debugPersistenceDirectoryFullPath;
   }
}
```

