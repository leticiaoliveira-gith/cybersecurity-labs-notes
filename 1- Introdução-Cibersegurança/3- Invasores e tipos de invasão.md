Este documento apresenta uma visão geral sobre os diferentes tipos de agentes de ameaças e os métodos utilizados para infiltração em sistemas.

## 1. Tipos de Invasores (Hackers)

A comunidade de segurança cibernética categoriza os invasores frequentemente com base em suas motivações e níveis de habilidade:

* **Script Kiddies:** Indivíduos com baixo nível de conhecimento técnico que utilizam ferramentas, *scripts* ou códigos prontos criados por terceiros para realizar ataques, sem compreender profundamente como o ataque funciona.
<img src="../.assets/kiddies.jpg" width="150" alt="Kiddies">

* **Hackers (Categorias):**
    * **White Hat (Éticos):** Profissionais contratados para encontrar vulnerabilidades e ajudar a proteger sistemas.
    <img src="../.assets/whiter.jpg" width="150" alt="white">
    
    * **Black Hat (Cibercriminosos):** Motivado por lucro, malícia ou ganho pessoal, atuando fora da lei.
    <img src="../.assets/black.jpg" width="150" alt="black">
    
    * **Grey Hat:** Ficam no meio termo, podendo realizar invasões sem autorização, mas sem a intenção direta de causar dano.
    <img src="../.assets/grey.jpg" width="150" alt="grey">

### Duas Áreas de Atuação Comuns
1.  **Segurança Ofensiva (Red Teaming / Pentesting):** Especialistas que simulam ataques reais para testar a resistência das defesas de uma organização.
2.  **Segurança Defensiva (Blue Teaming / SOC):** Especialistas responsáveis por monitorar, detectar e neutralizar ameaças, protegendo a infraestrutura contra ataques.

---

## 2. Métodos de Infiltração e Ataques

Os invasores utilizam diversas técnicas para comprometer sistemas, redes e usuários:

* **Engenharia Social:** Manipulação psicológica de pessoas para que elas revelem informações confidenciais ou realizem ações que comprometam a segurança.

* **Negação de Serviço (DoS):** Ataque que visa tornar um serviço ou recurso indisponível aos seus usuários legítimos, sobrecarregando o sistema.

* **Negação de Serviço Distribuída (DDoS):** Similar ao DoS, porém utiliza uma rede de computadores comprometidos (zumbis) para atacar um alvo de múltiplas fontes simultaneamente.

* **Botnet:** Uma rede de computadores infectados sob o controle de um invasor (o "botmaster"), usada para coordenar ataques em larga escala.

* **Ataque On-Path (Anteriormente Man-in-the-Middle):** O atacante intercepta a comunicação entre duas partes, podendo ler ou modificar os dados trocados sem que as vítimas percebam.

* **Man-in-the-Mobile (MitMo):** Uma forma de ataque *on-path* direcionada especificamente a dispositivos móveis, visando interceptar transações ou códigos de autenticação (como SMS/2FA).

* **SEO Poisoning:** Manipulação dos resultados de mecanismos de busca (como o Google) para direcionar usuários a sites maliciosos que instalam *malware* ou roubam dados.

* **Advanced Persistent Threat (APT):** Um ataque complexo e prolongado, onde o invasor obtém acesso a uma rede e permanece nela sem ser detectado por longos períodos para realizar espionagem ou exfiltração de dados.