[![CI](https://github.com/ktooi/ansible-role-slapd/workflows/CI/badge.svg)](https://github.com/ktooi/ansible-role-slapd/actions?query=workflow%3ACI+branch%3Amain)

# Ansible Role: slapd

RHEL/CentOS, Debian/Ubuntu サーバに slapd をインストールし、基本的な設定を行います。

## Requirements

この role には特別な要件はありません。

## Role Variables

```yaml
# Set this to the slapd global configurations.
slapd_loglevel: stats
# slapd_idletimeout: 86400
# slapd_sizelimit: 500
# slapd_referral: on
```

[OpenLDAP Software 2.4 Administrator's Guide: Configuring slapd](https://www.openldap.org/doc/admin24/slapdconf2.html#cn%3Dconfig)

```yaml
# Users credential.
slapd_passwd_scheme: '{SSHA}'
ldap_root_passwd: "root_passwd"
ldap_admin: "cn=admin"
# Set this if different from the ldap_basedn.
# ldap_admin_base: "dc=example,dc=com"
ldap_admin_passwd: "admin_passwd"
# If you want to reduce the number of tasks
# that are "Changed", specify the hash
# that you generated beforehand using the following slappasswd command.
# $ slappasswd -h '{SSHA}'
# ldap_root_hashed_passwd: '{SSHA}WA/exo2HKC1H4EsOUxGbWU6mW0eT1A1K'
# ldap_admin_hashed_passwd: '{SSHA}a5gsMFahundHCuqNYeVrhX3QO6ZXCI+/'
```

slapd の管理権限を設定します。

```yaml
# Select whether or not to install the schemas.
slapd_install_schema_cosine: true
slapd_install_schema_nis: true
slapd_install_schema_misc: false
slapd_install_schema_ssh_lpk: false
slapd_install_schema_sudo: false
```

インストールするスキーマを指定します。

`true` に設定することでスキーマがインストールされます。
`false` に設定するとスキーマはインストールされません。

一度インストールしたスキーマは、 `false` に設定してもアンインストールされません。

```yaml
# Select whether or not to install the modules.
slapd_install_module_refint: false
slapd_install_module_memberof: false
```

インストールするモジュールを指定します。
RHEL/CentOS 7 ではタスクに失敗するのでこれらの変数を `true` に設定してはいけません。

`true` に設定することでモジュールがインストールされます。
`false` に設定するとモジュールはインストールされません。

一度インストールしたモジュールは、 `false` に設定してもアンインストールされません。

## Dependencies

None.

## Example Playbook

```yaml
- hosts: ldap-servers
  vars_files:
    - vars/main.yml
  roles:
    - slapd
```

Inside `vars/main.yml` :

```yaml
ldap_basedn: dc=your,dc=domain,dc=example,dc=com
ldap_organization_name: Your Example Co., Ltd.

ldap_root_passwd: "root_passwd"
ldap_admin: "cn=Manager"
ldap_admin_passwd: "Manager_p@55w0rd"
```

```yaml
ldap_base_head: your
ldap_domain: your.domain.example.com
```

これらの変数の値は `ldap_basedn` から自動的に計算されますが、別の値を利用したい場合は定義してください。

## Authors

* **Kodai Tooi** [GitHub](https://github.com/ktooi), [Qiita](https://qiita.com/ktooi)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
