# There is some issue with installing drupal with existing config, 
# hence perform default site installation first
drush si

# Find UUID value from the file config/sync/system.site.yml or refer
# https://drupal.stackexchange.com/questions/150481/how-can-i-import-the-configuration-on-a-different-site/247495#247495
drush cset system.site uuid UUID_VALUE
drush drush cim -y

# (Optional) If any error related to Shortcut Link/Set
drush -y entity:delete shortcut_set
drush drush cim -y

# Get login link
drush uli

# For Oauth to work.
- Create a user with role 'Consumer React' at /admin/people/create
- Create a consumer with label 'Consumer React' at /admin/config/services/consumer/add
  - Add a password for the consumer using 'New Secret' field 
  - Select Scopes as 'Consumer React'
  - Save

In postman use 
- client_id as UUID against the consumer 'Consumer React' at admin/config/services/consumer
- client_secret as the password set for the 'Consumer React' consumer
