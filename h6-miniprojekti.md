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

Seuraavaksi luodaan hosts.ini tiedostot sekä ansible.cfg tiedostot.
<img width="416" height="82" alt="kuva" src="https://github.com/user-attachments/assets/3b48c3da-c960-402d-b98c-9b5d1ef53df8" />



<img width="715" height="100" alt="kuva" src="https://github.com/user-attachments/assets/6790dfb2-93c1-4316-8581-43d798cc2701" />

sekä viimeisenä site.yml tiedosto.

<img width="1092" height="183" alt="kuva" src="https://github.com/user-attachments/assets/c7499b30-f213-4f27-8055-2868ab0c7b4b" />

Tässä otetaan yhteys paikallisesti, koska olen lisänyt ssh-avaimen jo.

Seuraavaksi luodaan main.yml tiedosto komennolla `micro roles/media/tasks/main.yml`. ja rakenne näyttää siellä tältä.

<img width="790" height="116" alt="kuva" src="https://github.com/user-attachments/assets/9c9e2d57-9295-4d1a-8c42-96ac7df6a33c" />

Tässä on hyödynnetty ansible files dokumentin pohjaa hieman soveltaen. (ansible-builtin.file)


Lopuksi lisätään vielä loput hakemistot eli: elokuvat, sarjat ja musiikki. Käytännössä tässä noudatetaan samaa hakemistorakennetta kuin /srv/media hakemistorakenteen luomisessa.

<img width="834" height="424" alt="kuva" src="https://github.com/user-attachments/assets/7d1946ce-828e-4d3f-b142-b0bfa492c8e6" />

Sitten ansible-palybook ajoa, ja huomaamme muutokset, että uudet hakemistot ovat tullut käyttöön.

<img width="1096" height="226" alt="kuva" src="https://github.com/user-attachments/assets/be324dc1-cf85-4aca-be33-50a929e20c70" />

komennolla tree /srv/media näyttää, että hakemistot ollaan nyt lisätty. Sekä uudelleenajon idempotenssi.

<img width="731" height="119" alt="kuva" src="https://github.com/user-attachments/assets/db8c5642-c8eb-4e0f-9a69-aa2ff242c958" />

<img width="1093" height="279" alt="kuva" src="https://github.com/user-attachments/assets/e6f182a3-6cc5-456d-ba50-46ec235a9d39" />









## Lähteet
- ansible-builtin-file.ansible.builtin.file module – Manage files and file properties. Luettavissa: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/file_module.html. Luettu: 27.11.2026.
.- Karvinen 2026. SSH public key - Login without password. Luettavissa: https://terokarvinen.com/ssh-public-key-login-without-password/. Luettu: 27.11.2026.

