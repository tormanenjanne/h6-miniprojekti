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

Tässä on hyödynnetty ansible files dokumentin pohjaa hieman soveltaen. 
- path: luodaan tämä kyseinen hakemistopolku. srv on luoto tähän siksi, jotta se käsittelee tämän kyseisen palvelun tietoja (Linux filesystem hierarchy)
- state: Kohteena on hakemisto, ja se luo tämän hakemiston
- mode: määritellään oikeudet: omistajalle kaikki oikeudet (rwx), ryhmälle (rx) ja muille (rx)
(ansible-builtin.file)


Lopuksi lisätään vielä loput hakemistot eli: elokuvat, sarjat ja musiikki. Käytännössä tässä noudatetaan samaa hakemistorakennetta kuin /srv/media hakemistorakenteen luomisessa.

<img width="834" height="424" alt="kuva" src="https://github.com/user-attachments/assets/7d1946ce-828e-4d3f-b142-b0bfa492c8e6" />

Sitten ansible-palybook ajoa, ja huomaamme muutokset, että uudet hakemistot ovat tullut käyttöön.

<img width="1096" height="226" alt="kuva" src="https://github.com/user-attachments/assets/be324dc1-cf85-4aca-be33-50a929e20c70" />

komennolla tree /srv/media näyttää, että hakemistot ollaan nyt lisätty. Sekä uudelleenajon idempotenssi.

<img width="731" height="119" alt="kuva" src="https://github.com/user-attachments/assets/db8c5642-c8eb-4e0f-9a69-aa2ff242c958" />

<img width="1093" height="279" alt="kuva" src="https://github.com/user-attachments/assets/e6f182a3-6cc5-456d-ba50-46ec235a9d39" />

## Palomuurin asennus, http- ja https liikenteen salliminen sekä palomuurin käyttöönotto koneen käynnistäessä

Ajakaa komento `ansible-galaxy collectin list`, ja etsikää sieltä community general, Jos tämä löytyy, muita toimenpiteitä ei toistaiseksi tarvita.

<img width="410" height="32" alt="kuva" src="https://github.com/user-attachments/assets/2d0b856c-b4ce-4324-b380-f9aecf11422a" />

Jos tämä puuttuu, käyttäkää komentoa `ansible-galaxy collection install community.general`. Tämä komento asentaa **community general** työkalun, jos se ei ole valmiiksi asentunut ansiblen yhteydessä.

Luodaan uusi hakemistorakenne komennolla `mkdir -p ufw/tasks/`, ja sitten microssa main.yml tiedosto `micro roles/ufw/tasks/main.yml`

<img width="720" height="372" alt="kuva" src="https://github.com/user-attachments/assets/7effef8d-823b-429e-ade3-7a8dc4177472" />

-	Asennetaan apt:lla ufw eli palomuuri ja present varmistaa, että se on asennettu
-	http-liikenne: rule: sallitaan liikenne, port:  80 = http-portti, proto: käytetään tcp-protokollaa
-	https-liikenne: rule: sallitaan liikenne, port: 443=https-portti, proto: tcp-protokolla
-	aktivoidaan palomuuri: state: enabled: uudelleenlataa palomuurin, ja käynnistää palomuurin boottauksen yhteysessä. Default: deny: estää oletuksena saapuvan tai lähtevän liikennteen käytäntöjä (ansible.bultin.apt s.a;community.general.ufw s.a; Maneshwas 2025)

Lopuksi lisätää site.yml tiedostoon vielä ufw rooli `micro site.yml`

<img width="728" height="137" alt="kuva" src="https://github.com/user-attachments/assets/84cb9a23-44aa-4e88-bcdd-92f4e52b1d7f" />

Ansible-playbook ajossa huomaamme, että muutoksia on tullut.

<img width="711" height="227" alt="kuva" src="https://github.com/user-attachments/assets/1dfab8d3-9943-424e-9467-d68da85df502" />

Testataan vielä idempotenssi ajamalla playbook uudelleen.

<img width="728" height="206" alt="kuva" src="https://github.com/user-attachments/assets/7e96ef1b-fcba-43f6-a05b-267473214fcc" />

Lopuksi vielä varmistamme, että http- sekä https liikenne on sallittu, sekä palomuuri on päällä komennolla `sudo ufw status verbose`(ubuntu wiki). Huomaamme halutun lopputuloksen, että http- ja https liikenne on sallittu.

<img width="594" height="218" alt="kuva" src="https://github.com/user-attachments/assets/88755d37-4376-4ee3-b760-5ed8da930917" />


## Lähteet
- ansible.builtiin.apt s.a. ansible.builtiin.apt. Luettavissa: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/apt_module.html. Luettu: 28.11.2026.
- ansible-builtin-file.ansible.builtin.file module – Manage files and file properties. Luettavissa: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/file_module.html. Luettu: 27.11.2026.
- Community.general.uwf s.a. community.general.ufw module – Manage firewall with UFW. Luettavissa: https://docs.ansible.com/projects/ansible/latest/collections/community/general/ufw_module.html. Luettu: 28.11.2026.
- Maneshwat 2025. Setting up a firewall with ansible and UFW: Luettavissa: https://dev.to/lovestaco/setting-up-a-firewall-with-ansible-and-ufw-3p9j. Luettu: 28.11.2026.
- Ubuntu wiki s.a. UFW. Luettavissa: https://wiki.ubuntu.com/UFW. Luettu: 28.11.2026.
- Karvinen 2026. SSH public key - Login without password. Luettavissa: https://terokarvinen.com/ssh-public-key-login-without-password/. Luettu: 27.11.2026.
- Linux filesystem hierarchy. 1.19. /srv. Luettavissa: https://tldp.org/LDP/Linux-Filesystem-Hierarchy/html/srv.html. Luettu: 27.11.2026
  
  

