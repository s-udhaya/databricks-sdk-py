Providers
=========
.. py:class:: ProvidersAPI

    A data provider is an object representing the organization in the real world who shares the data. A
    provider contains shares which further contain the shared data.

    .. py:method:: create(name, authentication_type [, comment, recipient_profile_str])

        Usage:

        .. code-block::

            import time
            
            from databricks.sdk import WorkspaceClient
            
            w = WorkspaceClient()
            
            public_share_recipient = """{
                    "shareCredentialsVersion":1,
                    "bearerToken":"dapiabcdefghijklmonpqrstuvwxyz",
                    "endpoint":"https://sharing.delta.io/delta-sharing/"
                }
            """
            
            created = w.providers.create(name=f'sdk-{time.time_ns()}', recipient_profile_str=public_share_recipient)
            
            # cleanup
            w.providers.delete(name=created.name)

        Create an auth provider.
        
        Creates a new authentication provider minimally based on a name and authentication type. The caller
        must be an admin on the metastore.
        
        :param name: str
          The name of the Provider.
        :param authentication_type: :class:`AuthenticationType`
          The delta sharing authentication type.
        :param comment: str (optional)
          Description about the provider.
        :param recipient_profile_str: str (optional)
          This field is required when the __authentication_type__ is **TOKEN** or not provided.
        
        :returns: :class:`ProviderInfo`
        

    .. py:method:: delete(name)

        Delete a provider.
        
        Deletes an authentication provider, if the caller is a metastore admin or is the owner of the
        provider.
        
        :param name: str
          Name of the provider.
        
        
        

    .. py:method:: get(name)

        Usage:

        .. code-block::

            import time
            
            from databricks.sdk import WorkspaceClient
            
            w = WorkspaceClient()
            
            public_share_recipient = """{
                    "shareCredentialsVersion":1,
                    "bearerToken":"dapiabcdefghijklmonpqrstuvwxyz",
                    "endpoint":"https://sharing.delta.io/delta-sharing/"
                }
            """
            
            created = w.providers.create(name=f'sdk-{time.time_ns()}', recipient_profile_str=public_share_recipient)
            
            _ = w.providers.get(name=created.name)
            
            # cleanup
            w.providers.delete(name=created.name)

        Get a provider.
        
        Gets a specific authentication provider. The caller must supply the name of the provider, and must
        either be a metastore admin or the owner of the provider.
        
        :param name: str
          Name of the provider.
        
        :returns: :class:`ProviderInfo`
        

    .. py:method:: list( [, data_provider_global_metastore_id])

        Usage:

        .. code-block::

            from databricks.sdk import WorkspaceClient
            from databricks.sdk.service import sharing
            
            w = WorkspaceClient()
            
            all = w.providers.list(sharing.ListProvidersRequest())

        List providers.
        
        Gets an array of available authentication providers. The caller must either be a metastore admin or
        the owner of the providers. Providers not owned by the caller are not included in the response. There
        is no guarantee of a specific ordering of the elements in the array.
        
        :param data_provider_global_metastore_id: str (optional)
          If not provided, all providers will be returned. If no providers exist with this ID, no results will
          be returned.
        
        :returns: Iterator over :class:`ProviderInfo`
        

    .. py:method:: list_shares(name)

        Usage:

        .. code-block::

            import time
            
            from databricks.sdk import WorkspaceClient
            
            w = WorkspaceClient()
            
            public_share_recipient = """{
                    "shareCredentialsVersion":1,
                    "bearerToken":"dapiabcdefghijklmonpqrstuvwxyz",
                    "endpoint":"https://sharing.delta.io/delta-sharing/"
                }
            """
            
            created = w.providers.create(name=f'sdk-{time.time_ns()}', recipient_profile_str=public_share_recipient)
            
            shares = w.providers.list_shares(name=created.name)
            
            # cleanup
            w.providers.delete(name=created.name)

        List shares by Provider.
        
        Gets an array of a specified provider's shares within the metastore where:
        
        * the caller is a metastore admin, or * the caller is the owner.
        
        :param name: str
          Name of the provider in which to list shares.
        
        :returns: Iterator over :class:`ProviderShare`
        

    .. py:method:: update(name [, comment, owner, recipient_profile_str])

        Usage:

        .. code-block::

            import time
            
            from databricks.sdk import WorkspaceClient
            
            w = WorkspaceClient()
            
            public_share_recipient = """{
                    "shareCredentialsVersion":1,
                    "bearerToken":"dapiabcdefghijklmonpqrstuvwxyz",
                    "endpoint":"https://sharing.delta.io/delta-sharing/"
                }
            """
            
            created = w.providers.create(name=f'sdk-{time.time_ns()}', recipient_profile_str=public_share_recipient)
            
            _ = w.providers.update(name=created.name, comment="Comment for update")
            
            # cleanup
            w.providers.delete(name=created.name)

        Update a provider.
        
        Updates the information for an authentication provider, if the caller is a metastore admin or is the
        owner of the provider. If the update changes the provider name, the caller must be both a metastore
        admin and the owner of the provider.
        
        :param name: str
          The name of the Provider.
        :param comment: str (optional)
          Description about the provider.
        :param owner: str (optional)
          Username of Provider owner.
        :param recipient_profile_str: str (optional)
          This field is required when the __authentication_type__ is **TOKEN** or not provided.
        
        :returns: :class:`ProviderInfo`
        