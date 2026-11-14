# Public GitHub publication checklist

Before changing your new repository from **Private** to **Public**, review every item:

- [ ] Open **all 17 screenshots** and remove or mask anything you do not want public (private-network IPs, computer names, Windows account names, personal directories, unrelated browser tabs). Some screenshots visibly contain `192.168.x.x` addresses and local host/account identifiers.
- [ ] Review both reports for the same identifiers, personally identifying information, or content you do not intend to publish.
- [ ] Confirm there are **no credentials**, Wazuh admin passwords, API keys, certificates, agent enrollment keys or tokens. None were intentionally packaged.
- [ ] Keep full `/var/ossec/etc/client.keys`, `authd.pass`, private certificates, full agent `ossec.conf`, `.env` files and secret-bearing logs out of the repository.
- [ ] Verify XML examples contain **only** demonstration rule/config snippets. Do not treat `windows_agent_config_snippet.xml` as a complete drop-in config.
- [ ] Ensure all figures accurately represent your own lab. Do not characterize benign Notepad or Wazuh security checks as attacks.
- [ ] Check GitHub's web preview, especially README image links and PDF links.

**Privacy:** This archive intentionally preserves original screenshot pixels for evidence integrity, rather than silently changing them. Review/redact locally before publishing.

**Licensing:** No broad reuse license has been granted in this archive. Add a LICENSE file only if you choose to allow reuse.
