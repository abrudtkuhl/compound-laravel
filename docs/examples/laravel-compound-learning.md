# Example: `/laravel-compound` Learning

This example shows the expected shape for reusable Laravel learning capture.

````markdown
# Team Invitation Authorization

## Context

Team invitation routes accept a team identifier in the URL and create invitations through a controller action.

## Learning

Authorization must be checked against the route-bound team before creating an invitation. Authentication alone is not enough because users can belong to multiple teams or guess team IDs.

## Laravel Pattern

Use a `TeamPolicy::invite(User $user, Team $team)` method and call it from `StoreTeamInvitationRequest::authorize()` so validation and authorization stay together for the write request.

## Example

```php
public function authorize(): bool
{
    return $this->user()?->can('invite', $this->route('team')) ?? false;
}
```

## Verification

- Feature test: owner can invite a user to their team.
- Feature test: member from another team receives 403.
- Feature test: unauthenticated request redirects or returns 401 according to route type.

## References

- `app/Http/Requests/StoreTeamInvitationRequest.php`
- `app/Policies/TeamPolicy.php`
- `tests/Feature/TeamInvitationTest.php`
````
