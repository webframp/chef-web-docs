

=====================================================
client.rb
=====================================================

.. tag config_rb_client_27

A client.rb file is used to specify the configuration details for the chef-client.

* This file is loaded every time this executable is run
* On UNIX- and Linux-based machines, the default location for this file is ``/etc/chef/client.rb``; on Microsoft Windows machines, the default location for this file is ``C:\chef\client.rb``; use the ``--config`` option from the command line to change this location
* This file is not created by default
* When a client.rb file is present in the default location, the settings contained within that client.rb file will override the default configuration settings

.. end_tag

Settings
=====================================================
This configuration file has the following settings:

``add_formatter``
   A 3rd-party formatter. (See `nyan-cat <https://github.com/andreacampi/nyan-cat-chef-formatter>`_ for an example of a 3rd-party formatter.) Each formatter requires its own entry.

``audit_mode``
   Enable audit-mode. Set to ``audit-only`` to skip the converge phase of the chef-client run and only perform audits. Possible values: ``audit-only``, ``disabled``, and ``enabled``. Default value: ``disabled``.

``automatic_attribute_whitelist``
   A Hash that whitelists ``automatic`` attributes, preventing non-whitelisted attributes from being saved.

``cache_path``
   Optional. The home directory for the user that is running the chef-client as a non-root user.

``checksum_path``
   The location in which checksum files are stored. These are used to validate individual cookbook files, such as recipes. The checksum itself is stored in the Chef server database and is then compared to a file in the checksum path that has a filename identical to the checksum.

``chef_repo_path``
   The path to the chef-repo.

``chef_server_url``
   The URL for the Chef server. For example:

   .. code-block:: ruby

      https://localhost/organizations/ORG_NAME

``chef_zero.enabled``
   Enable chef-zero. This setting requires ``local_mode`` to be set to ``true``. Default value: ``false``.

``chef_zero.port``
   The port on which chef-zero is to listen. This value may be specified as a range; the chef-client will take the first available port in the range. For example ``10,20,30`` or ``10000-20000``. Default value: ``8889-9999``.

``client_key``
   The location of the file that contains the client key. Default value: ``/etc/chef/client.pem``.

``client_registration_retries``
   The number of times a chef-client is to attempt to register with a Chef server. Default value: ``5``.

``chef_gem_compile_time``
   Controls the phase during which a gem is installed on a node. Set to ``true`` to install a gem while the resource collection is being built (the "compile phase"). Set to ``false`` to install a gem while the chef-client is configuring the node (the "converge phase"). Recommended value: ``false``.

   .. note:: .. tag resource_package_chef_gem_attribute_compile_time

             .. This topic is hooked into client.rb topics, starting with 12.1, in addition to the resource reference pages.

             To suppress warnings for cookbooks authored prior to chef-client 12.1, use a ``respond_to?`` check to ensure backward compatibility. For example:

             .. code-block:: ruby

                chef_gem 'aws-sdk' do
                  compile_time false if respond_to?(:compile_time)
                end

             .. end_tag

``cookbook_path``
   The sub-directory for cookbooks on the chef-client. This value can be a string or an array of file system locations, processed in the specified order. The last cookbook is considered to override local modifications.

``cookbook_sync_threads``
   The number of helper threads available for parallel cookbook synchronization. Increasing this value **may** increase the frequency of gateway errors from the Chef server (503 and 504 errors). Decreasing this number reduces the frequency of gateway errors, if present. Default value: ``10``.

``data_bag_decrypt_minimum_version``
   The minimum required version of data bag encryption. Possible values: ``0``, ``1``, and ``2``. When all of the machines in an organization are running chef-client version 11.6 (or higher), it is recommended that this value be set to ``2``.

``data_bag_path``
   The location from which a data bag is loaded. Default value: ``/var/chef/data_bags``.

``default_attribute_whitelist``
   A Hash that whitelists ``default`` attributes, preventing non-whitelisted attributes from being saved.

``diff_disabled``
   Cause the chef-client to create a diff when changes are made to a file. Default value: ``false``.

``diff_filesize_threshold``
   The maximum size (in bytes) of a file for which the chef-client can create a diff. Default value: ``10000000``.

``diff_output_threshold``
   The maximum size (in bytes) of a diff file created by the chef-client. Default value: ``1000000``.

``disable_event_logger``
   Enable or disable sending events to the Microsoft Windows "Application" event log. When ``false``, events are sent to the Microsoft Windows "Application" event log at the start and end of a chef-client run, and also if a chef-client run fails. Set to ``true`` to disable event logging. Default value: ``true``.

``enable_reporting``
   Cause the chef-client to send data to the Chef server for use with Reporting.

``enable_reporting_url_fatals``
   Cause the chef-client run to fail when Reporting data cannot be sent to the Chef server (for any reason).

``enable_selinux_file_permission_fixup``
   SELinux environments only. Cause the chef-client to attempt to apply the correct file permissions to an updated file via the ``restorecon`` command. Set this value to ``false`` to prevent the chef-client from attempting this action.

``encrypted_data_bag_secret``
   The subdirectory in which encrypted data bag secrets are located.

``environment``
   The name of the environment.

``environment_path``
   The path to the environment. Default value: ``/var/chef/environments``.

``file_atomic_update``
   Apply atomic file updates to all resources. Set to ``true`` for global atomic file updates. Set to ``false`` for global non-atomic file updates. (Use the ``atomic_update`` setting on a per-resource basis to override this setting.) Default value: ``true``.

   .. warning:: .. tag notes_config_rb_no_file_atomic_update

                Changing this setting to ``false`` may cause file corruption, data loss, or instability. Use the ``atomic_update`` property on the **cookbook_file**, **file**, **remote_file**, and **template** resources to tune this behavior at the recipe level.

                .. end_tag

``file_backup_path``
   The location in which backup files are stored. If this value is empty, backup files are stored in the directory of the target file. Default value: ``/var/chef/backup``.

``file_cache_path``
   The location in which cookbooks (and other transient data) files are stored when they are synchronized. This value can also be used in recipes to download files with the **remote_file** resource.

``file_staging_uses_destdir``
   How file staging (via temporary files) is done. When ``true``, temporary files are created in the directory in which files will reside. When ``false``, temporary files are created under ``ENV['TMP']``. Default value: ``true``.

``ftp_proxy``
   The proxy server for FTP connections.

``ftp_proxy_pass``
   The password for the proxy server when the proxy server is using an FTP connection. Default value: ``nil``.

``ftp_proxy_user``
   The user name for the proxy server when the proxy server is using an FTP connection. Default value: ``nil``.

``group``
   The group that owns a process. This is required when starting any executable as a daemon. Default value: ``nil``.

``http_proxy``
   The proxy server for HTTP connections. Default value: ``nil``.

``http_proxy_pass``
   The password for the proxy server when the proxy server is using an HTTP connection. Default value: ``nil``.

``http_proxy_user``
   The user name for the proxy server when the proxy server is using an HTTP connection. Default value: ``nil``.

``http_retry_count``
   The number of retry attempts. Default value: ``5``.

``http_retry_delay``
   The delay (in seconds) between retry attempts. Default value: ``5``.

``https_proxy``
   The proxy server for HTTPS connections. Default value: ``nil``.

``https_proxy_pass``
   The password for the proxy server when the proxy server is using an HTTPS connection. Default value: ``nil``.

``https_proxy_user``
   The user name for the proxy server when the proxy server is using an HTTPS connection. Default value: ``nil``.

``interval``
   The frequency (in seconds) at which the chef-client runs. Default value: ``1800``.

``json_attribs``
   The path to a file that contains JSON data.

``listen``
   Run chef-zero in socketless mode. Set to ``false`` to disable port binding and HTTP requests on localhost.

``local_key_generation``
   Whether the Chef server or chef-client generates the private/public key pair. When ``true``, the chef-client generates the key pair, and then sends the public key to the Chef server. Default value: ``true``.

``local_mode``
   Run the chef-client in local mode. This allows all commands that work against the Chef server to also work against the local chef-repo.

``lockfile``
   The location of the chef-client lock file. This value is typically platform-dependent, so should be a location defined by ``file_cache_path``. The default location of a lock file should not on an NF mount. Default value: a location defined by ``file_cache_path``.

``log_level``
   The level of logging to be stored in a log file. Possible levels: ``:auto`` (default), ``:debug``, ``:info``, ``:warn``, ``:error``, or ``:fatal``. Default value: ``:warn`` (when a terminal is available) or ``:info`` (when a terminal is not available).

``log_location``
   The location of the log file. Possible values: ``/path/to/log_location``, ``STDOUT``, ``STDERR``, ``Chef::Log::WinEvt.new`` (Windows Event Logger), or ``Chef::Log::Syslog.new('chef-client', ::Syslog::LOG_DAEMON)`` (writes to the syslog daemon facility with the originator set as ``chef-client``). The application log will specify the source as ``Chef``. Default value: ``STDOUT``.

``minimal_ohai``
   Run the Ohai plugins for name detection and resource/provider selection and no other Ohai plugins. Set to ``true`` during integration testing to speed up test cycles.

``no_lazy_load``
   Download all cookbook files and templates at the beginning of the chef-client run. Default value: ``true``.

``no_proxy``
   A comma-separated list of URLs that do not need a proxy. Default value: ``nil``.

``node_name``
   The name of the node. Determines which configuration should be applied and sets the ``client_name``, which is the name used when authenticating to a Chef server. The default value is the FQDN of the chef-client, as detected by Ohai. In general, Chef recommends that you leave this setting blank and let Ohai assign the FQDN of the node as the ``node_name`` during each chef-client run.

``node_path``
   The location in which nodes are stored when the chef-client is run in local mode. Default value: ``/var/chef/node``.

``normal_attribute_whitelist``
   A Hash that whitelists ``normal`` attributes, preventing non-whitelisted attributes from being saved.

``override_attribute_whitelist``
   A Hash that whitelists ``override`` attributes, preventing non-whitelisted attributes from being saved.

``pid_file``
   The location in which a process identification number (pid) is saved. An executable, when started as a daemon, writes the pid to the specified file. Default value: ``/tmp/name-of-executable.pid``.

``policy_group``
   The name of a policy, as identified by the ``name`` setting in a Policyfile.rb file. ``policy_name`` must also be specified.

``policy_name``
   The name of a policy group that exists on the Chef server. ``policy_group`` must also be specified.

``rest_timeout``
   The time (in seconds) after which an HTTP REST request is to time out. Default value: ``300``.

``role_path``
   The location in which role files are located. Default value: ``/var/chef/roles``.

``run_lock_timeout``
   The amount of time (in seconds) to wait for a chef-client lock file to be deleted. A chef-client run will not start when a lock file is present. If a lock file is not deleted before this time expires, the pending chef-client run will exit. Default value: not set (indefinite). Set to ``0`` to cause a second chef-client to exit immediately.

``splay``
   A random number between zero and ``splay`` that is added to ``interval``. Use splay to help balance the load on the Chef server by ensuring that many chef-client runs are not occuring at the same interval. Default value: ``nil``.

``ssl_ca_file``
   The file in which the OpenSSL key is saved. This setting is generated automatically by the chef-client and most users do not need to modify it.

``ssl_ca_path``
   The path to where the OpenSSL key is located. This setting is generated automatically by the chef-client and most users do not need to modify it.

``ssl_client_cert``
   The OpenSSL X.509 certificate used for mutual certificate validation. This setting is only necessary when mutual certificate validation is configured on the Chef server. Default value: ``nil``.

``ssl_client_key``
   The OpenSSL X.509 key used for mutual certificate validation. This setting is only necessary when mutual certificate validation is configured on the Chef server. Default value: ``nil``.

``ssl_verify_mode``
   Set the verify mode for HTTPS requests.

   * Use ``:verify_none`` to do no validation of SSL certificates.
   * Use ``:verify_peer`` to do validation of all SSL certificates, including the Chef server connections, S3 connections, and any HTTPS **remote_file** resource URLs used in the chef-client run. This is the recommended setting.

   Depending on how OpenSSL is configured, the ``ssl_ca_path`` may need to be specified. Default value: ``:verify_peer``.

``syntax_check_cache_path``
   All files in a cookbook must contain valid Ruby syntax. Use this setting to specify the location in which knife caches information about files that have been checked for valid Ruby syntax.

``umask``
   The file mode creation mask, or umask. Default value: ``0022``.

``user``
   The user that owns a process. This is required when starting any executable as a daemon. Default value: ``nil``.

``validation_client_name``
   The name of the chef-validator key that is used by the chef-client to access the Chef server during the initial chef-client run.

``validation_key``
   The location of the file that contains the key used when a chef-client is registered with a Chef server. A validation key is signed using the ``validation_client_name`` for authentication. Default value: ``/etc/chef/validation.pem``.

``verbose_logging``
   Set the log level. Options: ``true``, ``nil``, and ``false``. When this is set to ``false``, notifications about individual resources being processed are suppressed (and are output at the ``:info`` logging level). Setting this to ``false`` can be useful when a chef-client is run as a daemon. Default value: ``nil``.

``verify_api_cert``
   Verify the SSL certificate on the Chef server. When ``true``, the chef-client always verifies the SSL certificate. When ``false``, the chef-client uses the value of ``ssl_verify_mode`` to determine if the SSL certificate requires verification. Default value: ``false``.

``whitelist``
   A Hash that contains the whitelist used by Chef push jobs. For example:

   .. code-block:: ruby

      whitelist {
        'job-name' => 'command',
        'job-name' => 'command',
        'chef-client' => 'chef-client'
      }

   A job entry may also be ``'job-name' => {:lock => true}``, which will check the ``lockfile`` setting in the client.rb file before starting the job.

   .. warning:: The ``whitelist`` setting is available only when using Chef push jobs, a tool that runs jobs against nodes in an organization.

``windows_service.watchdog_timeout``
   The maximum amount of time (in seconds) available to the chef-client run when the chef-client is run as a service on the Microsoft Windows platform. If the chef-client run does not complete within the specified timeframe, the chef-client run is terminated. Default value: ``2 * (60 * 60)``.

``yum_lock_timeout``
   The amount of time (in seconds) after which a Yum lock request is to time out. Default value: ``30``.

Automatic Proxy Config
-----------------------------------------------------
.. tag proxy_env

If ``http_proxy``, ``https_proxy``, ``ftp_proxy``, or ``no_proxy`` is set in the client.rb file, the chef-client will configure the ``ENV`` variable based on these (and related) settings. For example:

.. code-block:: ruby

   http_proxy 'http://proxy.example.org:8080'
   http_proxy_user 'myself'
   http_proxy_pass 'Password1'

will be set to:

.. code-block:: ruby

   ENV['http_proxy'] = 'http://myself:Password1@proxy.example.org:8080'

.. end_tag

Ohai Settings
=====================================================

.. tag config_rb_ohai

Ohai configuration settings can be added to the client.rb file.

.. end_tag

.. tag 4_ohai_settings

``Ohai::Config[:directory]``
   The directory in which Ohai plugins are located.

``Ohai::Config[:disabled_plugins]``
   An array of Ohai plugins to be disabled on a node. The list of plugins included in Ohai can be found in the ``ohai/lib/ohai/plugins`` directory. For example, disabling a single plugin:

   .. code-block:: ruby

      Ohai::Config[:disabled_plugins] = [
        :MyPlugin
      ]

    or disabling multiple plugins:

   .. code-block:: ruby

      Ohai::Config[:disabled_plugins] = [
        :MyPlugin, 
        :MyPlugin, 
        :MyPlugin
      ]

   and to disable multiple plugins, including Ohai 6 plugins:

   .. code-block:: ruby

      Ohai::Config[:disabled_plugins] = [
		:MyPlugin, 
        :MyPlugin, 
        'my_ohai_6_plugin'
      ]

   When a plugin is disabled, the chef-client log file will contain entries similar to:

   .. code-block:: ruby

      [2014-06-13T23:49:12+00:00] DEBUG: Skipping disabled plugin MyPlugin

``Ohai::Config[:hints_path]``
   The path to the file that contains hints for Ohai.

``Ohai::Config[:log_level]``
   The level of logging to be stored in a log file.

``Ohai::Config[:log_location]``
   The location of the log file.

``Ohai::Config[:plugin_path]``
   An array of paths at which Ohai plugins are located. Default value: ``[<CHEF_GEM_PATH>/ohai-9.9.9/lib/ohai/plugins]``. When custom Ohai plugins are added, the paths must be added to the array. For example, a single plugin:

   .. code-block:: ruby

      Ohai::Config[:plugin_path] << '/etc/chef/ohai_plugins'

   and for multiple plugins:

   .. code-block:: ruby

      Ohai::Config[:plugin_path] += [
        '/etc/chef/ohai_plugins',
        '/path/to/other/plugins'
        ]

``Ohai::Config[:version]``
   The version of Ohai.

.. note:: The Ohai executable ignores settings in the client.rb file when Ohai is run independently of the chef-client.

.. end_tag

Example
=====================================================
.. tag config_rb_client_example

A sample client.rb file that contains the most simple way to connect to https://manage.chef.io:

.. code-block:: ruby

   log_level        :info
   log_location     STDOUT
   chef_server_url  'https://api.opscode.com/organizations/<orgname>'
   validation_client_name '<orgname>-validator'
   validation_key '/etc/chef/validator.pem'
   client_key '/etc/chef/client.pem'

.. end_tag

