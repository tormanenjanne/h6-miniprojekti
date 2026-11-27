## h6-miniprojekti

## Mediahakemistojen luominen

Aloitetaan asentamalla ansible, micro, tree,bash sekä git, tämä onnistuu komennolla.

```markdown
sudo apt-get install ansible micro bash-completion tree git
```
Tämän jälkeen luodaan ssh-avainpari komennolla

```markdown
ssh-keygen
```

Muutamalla entterin painnalluksella, saadaan luotua ssh-avainparit. Tämän jälkeen kopiodaan ssh-avaimet yhteiselle repositorille, ja kloonataan repository virtuaalikoneelle.

```markdown
git clone git@github.com:tormanenjanne/h6-miniprojekti.git
```

Seuraavaksi luodaan host.ini tiedostot sekä ansible.cfg tiedostot.
<img width="416" height="82" alt="kuva" src="https://github.com/user-attachments/assets/3b48c3da-c960-402d-b98c-9b5d1ef53df8" />

<img width="1082" height="88" alt="kuva" src="https://github.com/user-attachments/assets/34d820ef-df99-4b82-bba9-b2157f2e8590" />

sekä viimeisenä site.yml tiedosto.

<img width="1092" height="183" alt="kuva" src="https://github.com/user-attachments/assets/c7499b30-f213-4f27-8055-2868ab0c7b4b" />






## Lähteet

- Karvinen 2026. SSH public key - Login without password. Luettavissa: https://terokarvinen.com/ssh-public-key-login-without-password/. Luettu: 27.11.2026.

