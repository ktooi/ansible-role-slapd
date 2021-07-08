# Ansible Role: slapd

Debian/Ubuntu サーバに slapd をインストールし、基本的な設定を行います。

## Requirements

この role には特別な要件はありません。

## Role Variables

TBA

## Dependencies

None.

## Example Playbook

```
- hosts: ldap-servers
  vars_files:
    - vars/main.yml
  roles:
    - slapd
```

Inside `vars/main.yml` :

```
ldap_basedn: dc=your,dc=domain,dc=example,dc=com
ldap_base_head: your
ldap_organization_name: Your Example Co., Ltd.
ldap_domain: your.domain.example.com

ldap_root_passwd: "root_passwd"
ldap_admin: "cn=Manager"
ldap_admin_passwd: "Manager_p@55w0rd"
```

## Authors

*   **Kodai Tooi** [GitHub](https://github.com/ktooi), [Qiita](https://qiita.com/ktooi)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
