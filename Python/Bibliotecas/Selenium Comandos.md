

# Selenium com Python (Comandos Comuns e Exemplos Práticos)

Principais recomendações no topo:

- Use locators estáveis (id/data-testid) e esperas explícitas com WebDriverWait para sincronização confiável.
- Evite time.sleep() no fluxo crítico; prefira condições como “element_to_be_clickable” e “visibility_of_element_located”.
- Organize o código com Page Object Model (POM) para manutenibilidade e reuso.


## 1) Conceitos e Setup

Selenium WebDriver permite automatizar navegadores (Chrome, Firefox, Edge, Safari). Através das bindings de Python é possível navegar por páginas, localizar elementos e executar interações robustas, controlando janelas, iframes, abas, alertas, cookies e ações avançadas. O primeiro passo é instalar o pacote selenium e ter um WebDriver compatível com o navegador desejado.

Instalação:

- pip install -U selenium

Exemplo mínimo:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://exemplo.com")
campo = driver.find_element(By.NAME, "q")
campo.send_keys("Selenium")
driver.quit()
```

Boas práticas de ambiente:

- Utilize venv para isolar dependências.
- Defina versões do WebDriver de forma previsível; em CI, prefira headless.


## 2) Navegação e Controle do Navegador

Comandos comuns do driver:

- Navegação: get(url), back(), forward(), refresh()
- Informações: title, current_url, page_source
- Janela: maximize_window(), set_window_size(l, a)
- Timeout implícito: implicitly_wait(segundos) (use com cautela; prefira esperas explícitas)

Exemplo:

```python
driver.get("https://www.selenium.dev/selenium/web/web-form.html")
print(driver.title)
driver.back()
driver.forward()
driver.refresh()
driver.maximize_window()
```


## 3) Localização de Elementos (Locators)

Estratégias de localização via By:

- Básicos: ID, NAME, CLASS_NAME, TAG_NAME
- Texto de links: LINK_TEXT, PARTIAL_LINK_TEXT
- Poderosos: CSS_SELECTOR, XPATH

Diferenças:

- find_element(...) lança exceção se não encontrar.
- find_elements(...) retorna lista (vazia se não houver correspondência).

Exemplos:

```python
from selenium.webdriver.common.by import By

el = driver.find_element(By.ID, "username")
itens = driver.find_elements(By.CSS_SELECTOR, "ul.items > li")
btn = driver.find_element(By.XPATH, "//button[@type='submit']")
label = driver.find_element(By.XPATH, "//*[text()='Enviar']")
```

Boas práticas de locators:

- Prefira IDs estáveis ou atributos data-*.
- CSS é legível e performático; XPath para casos complexos (texto, hierarquias).
- Evite seletores frágeis (classes geradas, indexação instável).


## 4) Interações com WebElement

Métodos úteis:

- click(), send_keys(), clear()
- text (texto visível), get_attribute("name")
- is_displayed(), is_enabled(), is_selected()
- value_of_css_property("prop")

Exemplo preenchendo formulário:

```python
user = driver.find_element(By.NAME, "user")
pwd = driver.find_element(By.NAME, "pass")
submit = driver.find_element(By.CSS_SELECTOR, "button[type='submit']")

user.clear(); user.send_keys("usuario")
pwd.clear(); pwd.send_keys("segredo")
submit.click()
```


## 5) Esperas: Implícitas, Explícitas e Fluent

- Implícitas: driver.implicitly_wait(s) – afetam todas as buscas, podem mascarar problemas.
- Explícitas: WebDriverWait + expected_conditions (recomendado).
- Fluent: variação da explícita (intervalo de polling, exceções ignoradas).

Exemplo com WebDriverWait:

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
el = wait.until(EC.presence_of_element_located((By.ID, "resultado")))
btn = wait.until(EC.element_to_be_clickable((By.CSS_SELECTOR, "button.enviar")))
btn.click()
```

Condições úteis:

- presence_of_element_located, visibility_of_element_located
- element_to_be_clickable
- text_to_be_present_in_element
- url_contains
- frame_to_be_available_and_switch_to_it


## 6) Ações Avançadas (ActionChains)

Para gestos compostos: hover, drag-and-drop, cliques com modificadores, digitação com teclas especiais.

Exemplo:

```python
from selenium.webdriver import ActionChains
from selenium.webdriver.common.keys import Keys

menu = driver.find_element(By.ID, "menu")
alvo = driver.find_element(By.ID, "alvo")

ActionChains(driver).move_to_element(menu).click_and_hold().move_to_element(alvo).release().perform()

campo = driver.find_element(By.ID, "campo")
ActionChains(driver).click(campo).key_down(Keys.SHIFT).send_keys("abc").key_up(Keys.SHIFT).perform()
```


## 7) <select> e Dropdowns

Use Select para listas suspensas nativas:

```python
from selenium.webdriver.support.ui import Select

select = Select(driver.find_element(By.ID, "estado"))
select.select_by_visible_text("São Paulo")
select.select_by_value("SP")
select.select_by_index(3)
```


## 8) Iframes

Troca de contexto é obrigatória para interagir com iframes:

```python
iframe = driver.find_element(By.CSS_SELECTOR, "iframe#editor")
driver.switch_to.frame(iframe)
# ... interações ...
driver.switch_to.default_content()
```


## 9) Abas e Janelas

Abrindo nova aba e alternando:

```python
driver.execute_script("window.open('about:blank','_blank');")
abas = driver.window_handles
driver.switch_to.window(abas[-1])
driver.close()
driver.switch_to.window(abas[^0])
```


## 10) Alertas e Diálogos

```python
from selenium.common.exceptions import NoAlertPresentException

try:
    alert = driver.switch_to.alert
    print(alert.text)
    alert.accept()  # ou dismiss()
except NoAlertPresentException:
    pass
```


## 11) Execução de JavaScript

```python
titulo = driver.execute_script("return document.title;")
driver.execute_script("arguments[^0].scrollIntoView(true);", el)
driver.execute_script("arguments[^0].click();", el)
```


## 12) Cookies 

```python
cookies = driver.get_cookies()
driver.add_cookie({"name": "token", "value": "abc123"})
driver.delete_cookie("token")
driver.delete_all_cookies()
```


## 13) Headless e Multinavegador

Chrome headless:

```python
from selenium.webdriver.chrome.options import Options

opts = Options()
opts.add_argument("--headless=new")
opts.add_argument("--window-size=1920,1080")
driver = webdriver.Chrome(options=opts)
```

Firefox headless:

```python
from selenium.webdriver.firefox.options import Options as FFOptions

opts = FFOptions()
opts.add_argument("-headless")
driver = webdriver.Firefox(options=opts)
```

Boas práticas:

- Parametrize navegador/timeouts por config (JSON/env).
- Use implicitly_wait baixo (0–2s) e baseie lógica em esperas explícitas.


## 14) Page Object Model (POM)

Separar responsabilidades melhora manutenção e reuso.

Exemplo:

```python
# pages/login_page.py
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class LoginPage:
    USER = (By.ID, "username")
    PASS = (By.ID, "password")
    SUBMIT = (By.CSS_SELECTOR, "button[type='submit']")

    def __init__(self, driver):
        self.driver = driver
        self.wait = WebDriverWait(driver, 10)

    def open(self):
        self.driver.get("https://app.exemplo.com/login")

    def login(self, user, pwd):
        self.wait.until(EC.visibility_of_element_located(self.USER)).send_keys(user)
        self.driver.find_element(*self.PASS).send_keys(pwd)
        self.driver.find_element(*self.SUBMIT).click()
```


## 15) Erros Comuns e Mitigações

- NoSuchElementException: locator incorreto ou timing – use esperas explícitas e valide a visibilidade.
- ElementClickInterceptedException: elemento sobreposto – role até o alvo, aguarde clicabilidade, remova overlays.
- StaleElementReferenceException: re-render – relocalize o elemento antes de interagir.
- TimeoutException: condição não cumprida – revise condição/timeout e sinalizadores de conclusão (spinners, banners).

Padrão de reintento:

```python
from selenium.common.exceptions import StaleElementReferenceException

for _ in range(3):
    try:
        el = driver.find_element(By.ID, "dinamico")
        el.click()
        break
    except StaleElementReferenceException:
        continue
```


## 16) Upload e Download

Upload via input file:

```python
inp = driver.find_element(By.CSS_SELECTOR, "input[type='file']")
inp.send_keys(r"C:\caminho\arquivo.pdf")
```

Download em headless:

- Configure preferências de download via opções do navegador (pasta, prompts) conforme o driver.


## 17) Execução Remota e Grid

```python
from selenium.webdriver import Remote
from selenium.webdriver.chrome.options import Options

opts = Options(); opts.add_argument("--headless=new")
driver = Remote(command_executor="http://grid:4444/wd/hub", options=opts)
```


## 18) Exemplos Práticos Integrados

Login e verificação:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

with webdriver.Chrome() as driver:
    wait = WebDriverWait(driver, 10)
    driver.get("https://app.exemplo.com/login")

    wait.until(EC.visibility_of_element_located((By.ID, "username"))).send_keys("user")
    driver.find_element(By.ID, "password").send_keys("senha")
    driver.find_element(By.CSS_SELECTOR, "button[type='submit']").click()

    msg = wait.until(EC.visibility_of_element_located((By.ID, "welcome"))).text
    assert "Bem-vindo" in msg
```

Tabela dinâmica:

```python
wait.until(EC.invisibility_of_element_located((By.CSS_SELECTOR, ".spinner")))
linhas = driver.find_elements(By.CSS_SELECTOR, "table#produtos tbody tr")
assert len(linhas) > 0
```

Drag-and-drop:

```python
from selenium.webdriver import ActionChains

src = driver.find_element(By.ID, "card-A")
dst = driver.find_element(By.ID, "coluna-B")
ActionChains(driver).drag_and_drop(src, dst).perform()

assert "card-A" in dst.get_attribute("innerHTML")
```

Iframe + Select + Espera:

```python
driver.switch_to.frame(driver.find_element(By.CSS_SELECTOR, "iframe#checkout"))
Select(driver.find_element(By.ID, "parcelas")).select_by_value("3")
wait.until(EC.text_to_be_present_in_element((By.ID, "resumo"), "3x"))
driver.switch_to.default_content()
```

Reintento de clique:

```python
from selenium.common.exceptions import ElementClickInterceptedException

btn = (By.CSS_SELECTOR, "button.salvar")
for _ in range(3):
    try:
        el = wait.until(EC.element_to_be_clickable(btn))
        el.click()
        break
    except ElementClickInterceptedException:
        driver.execute_script("arguments[^0].scrollIntoView(true);", el)
```


## 19) Checklist de Estabilidade e Manutenção

- Locators confiáveis (IDs/data-testid).
- Esperas explícitas em cada transição/ação.
- Sem sleeps fixos no fluxo principal.
- Evidências de falha (screenshots, HTML, logs).
- POM para reuso e clareza.
- Headless consistente no CI com window-size definido.
- Testes curtos, determinísticos e independentes.

***

## Referências

1. [Write your first Selenium script][^1]
2. [Actions API][^2]
3. [Locator strategies][^3]
4. [Selenium with Python - Read the Docs][^4]
5. [Selenium Python Bindings (PDF em Read the Docs)][^5]
6. [WebDriver API — Selenium Python Bindings][^6]
7. [Waits — Selenium Python Bindings][^7]
8. [Getting Started — Selenium Python Bindings][^8]
9. [Find Elements in Selenium with Python][^9]
10. [Selenium Wait Commands using Python][^10]
11. [Modern Web Automation With Python and Selenium][^11]
12. [Selenium Python Tutorial (RealPython overview avançado)][^11]
13. [Selenium With Python for Automated Testing (Sauce Labs)][^12]
14. [Selenium Python Tutorial (BrowserStack)][^13]
15. [Locators in Selenium: A Detailed Guide][^14]
16. [Selenium para iniciantes: tutorial completo][^15]
17. [Automação Web com Python e Selenium (BotCity - PT-BR)][^16]
18. [Web Automation with Python and Selenium (BotCity - EN)][^17]
19. [Selenium Webdriver com Python - Tutorial PT-BR][^18]
20. [Configuring Multiple Browsers with Selenium and Python][^19]
21. [FindElement vs findElements (conceitos e diferenças)][^20]
22. [Selenium Wait Commands - GeeksforGeeks][^21]
23. [Element methods in Selenium Python - GeeksforGeeks][^22]
24. [Locator Strategies - Selenium Python - GeeksforGeeks][^23]
25. [Wait until page is loaded with Selenium WebDriver for Python][^24]
26. [Selenium com Python: tutorial completo (Asimov Academy)][^25]
27. [Selenium Python Bindings (PyPI - informações de pacote)][^26]
28. [Sobre automação de testes (Documentação Selenium PT-BR)][^27]
29. [Como usar Selenium para raspagem da web - Bright Data][^28]
30. [Selenium Python Tutorial for Beginners (TestGrid)][^29]
<span style="display:none">[^100][^101][^102][^103][^104][^105][^106][^107][^30][^31][^32][^33][^34][^35][^36][^37][^38][^39][^40][^41][^42][^43][^44][^45][^46][^47][^48][^49][^50][^51][^52][^53][^54][^55][^56][^57][^58][^59][^60][^61][^62][^63][^64][^65][^66][^67][^68][^69][^70][^71][^72][^73][^74][^75][^76][^77][^78][^79][^80][^81][^82][^83][^84][^85][^86][^87][^88][^89][^90][^91][^92][^93][^94][^95][^96][^97][^98][^99]</span>

<div align="center">⁂</div>

[^1]: https://www.selenium.dev/documentation/webdriver/getting_started/first_script/

[^2]: https://www.selenium.dev/documentation/webdriver/actions_api/

[^3]: https://www.selenium.dev/documentation/webdriver/elements/locators/

[^4]: https://selenium-python.readthedocs.io

[^5]: https://readthedocs.org/projects/selenium-python/downloads/pdf/latest/

[^6]: https://selenium-python.readthedocs.io/api.html

[^7]: https://selenium-python.readthedocs.io/waits.html

[^8]: https://selenium-python.readthedocs.io/getting-started.html

[^9]: https://www.browserstack.com/guide/find-element-in-selenium-with-python

[^10]: https://www.browserstack.com/guide/selenium-wait-commands-using-python

[^11]: https://realpython.com/modern-web-automation-with-python-and-selenium/

[^12]: https://saucelabs.com/resources/blog/selenium-with-python-for-automated-testing

[^13]: https://www.browserstack.com/guide/python-selenium-to-run-web-automation-test

[^14]: https://www.browserstack.com/guide/locators-in-selenium

[^15]: https://didatica.tech/selenium-para-iniciantes-tutorial-completo/

[^16]: https://blog.botcity.dev/pt-br/2024/02/12/automacao-web-python/

[^17]: https://blog.botcity.dev/2024/02/12/web-automation-python/

[^18]: https://www.luizdeaguiar.com.br/pt/2022/02/selenium-webdriver-com-python/

[^19]: https://www.luizdeaguiar.com.br/2022/03/configuring-multiple-browsers-with-selenium-and-python/

[^20]: https://testgrid.io/blog/findelement-vs-findelements-selenium/

[^21]: https://www.geeksforgeeks.org/software-testing/waits-in-selenium-python/

[^22]: https://www.geeksforgeeks.org/python/element-methods-in-selenium-python/

[^23]: https://www.geeksforgeeks.org/python/locator-strategies-selenium-python/

[^24]: https://stackoverflow.com/questions/26566799/wait-until-page-is-loaded-with-selenium-webdriver-for-python

[^25]: https://hub.asimov.academy/tutorial/guia-basico-de-selenium-com-python/

[^26]: https://pypi.org/project/selenium/

[^27]: https://www.selenium.dev/pt-br/documentation/test_practices/overview/

[^28]: https://brightdata.com.br/blog/procedimentos/using-selenium-for-web-scraping

[^29]: https://testgrid.io/blog/python-selenium-tutorial/

[^30]: https://openbooks.kb.dk/au/catalog/book/539

[^31]: http://journals.khnu.km.ua/vestnik/?p=16776

[^32]: https://dl.acm.org/doi/10.1145/3627673.3679217

[^33]: https://pubs2.ascee.org/index.php/viperarts/article/view/1633

[^34]: https://academic.oup.com/bioinformatics/article/doi/10.1093/bioinformatics/btac757/6847088

[^35]: https://academic.oup.com/bioinformatics/article/doi/10.1093/bioinformatics/btae700/7905459

[^36]: https://iopscience.iop.org/article/10.3847/1538-3881/aafc33

[^37]: https://academic.oup.com/bioinformaticsadvances/article/doi/10.1093/bioadv/vbae207/7932119

[^38]: https://academic.oup.com/bioinformaticsadvances/article/doi/10.1093/bioadv/vbae185/7907200

[^39]: https://pubs.geoscienceworld.org/srl/article/96/5/3231/654285/surfQuake-A-New-Python-Toolbox-for-the-Workflow

[^40]: https://astesj.com/?download_id=12611\&smd_process_download=1

[^41]: https://arxiv.org/pdf/2206.06428.pdf

[^42]: https://arxiv.org/pdf/2402.01480.pdf

[^43]: https://www.mdpi.com/2076-3921/12/11/1906

[^44]: https://www.mdpi.com/1420-3049/27/19/6613/pdf?version=1665367052

[^45]: https://brightdata.com.br/faqs/selenium/what-is-selenium

[^46]: https://www.dio.me/articles/o-que-e-selenium-em-python

[^47]: https://www.youtube.com/watch?v=NB8OceGZGjA

[^48]: https://pt.stackoverflow.com/questions/216385/web-scraping-selenium-python-em-site-com-geração-dinâmica-via-js-dificuldade

[^49]: https://www.youtube.com/watch?v=X73Iyq1M688

[^50]: https://www.selenium.dev/selenium-ide/docs/en/api/commands

[^51]: https://hub.asimov.academy/blog/selenium-com-python-tutorial-completo-para-automacao/

[^52]: https://ics60.aait.od.ua/zbirnik2024.pdf

[^53]: https://link.springer.com/10.1007/s11033-023-08242-6

[^54]: https://mobilednajournal.biomedcentral.com/articles/10.1186/s13100-023-00296-4

[^55]: https://www.frontiersin.org/articles/10.3389/fnut.2025.1683556/full

[^56]: https://ieeexplore.ieee.org/document/9950697/

[^57]: https://joss.theoj.org/papers/10.21105/joss.02879

[^58]: http://dergipark.org.tr/en/doi/10.53446/actamednicomedia.1243239

[^59]: https://publicacoes.softaliza.com.br/cilamce/article/view/10392

[^60]: https://saemobilus.sae.org/papers/fatigue-life-analysis-methods-rolling-lobe-air-spring-2024-01-2259

[^61]: http://biorxiv.org/lookup/doi/10.1101/2023.01.27.525916

[^62]: https://pmc.ncbi.nlm.nih.gov/articles/PMC1568638/

[^63]: https://www.mdpi.com/1420-3049/29/4/801/pdf?version=1707465507

[^64]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10227571/

[^65]: https://www.mdpi.com/1424-8220/23/22/9187/pdf?version=1700017463

[^66]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10674224/

[^67]: https://www.mdpi.com/2072-6643/14/17/3530/pdf?version=1661573315

[^68]: https://www.mdpi.com/2073-4441/13/11/1473/pdf

[^69]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10362088/

[^70]: https://testautomationu.applitools.com/selenium-webdriver-python-tutorial/chapter7.html

[^71]: https://blog.apify.com/selenium-find-elements/

[^72]: https://jurnal.polgan.ac.id/index.php/sinkron/article/view/13569

[^73]: https://journals.lww.com/10.1519/SSC.0000000000000800

[^74]: https://isjem.com/download/evaluating-selenium-4-features-and-their-impact-on-web-automation-testing-with-javascript/

[^75]: https://www.semanticscholar.org/paper/473e5bc1937d9450d43e12badbfcbb0f5e4bea59

[^76]: https://resmilitaris.net/index.php/resmilitaris/article/view/4455

[^77]: https://ieeexplore.ieee.org/document/10982654/

[^78]: https://www.humankineticslibrary.com/encyclopedia?docid=b-9781718218765

[^79]: https://journals.nmetau.edu.ua/index.php/st/article/view/2048

[^80]: https://www.nature.com/articles/s41598-024-79720-5

[^81]: https://aacnjournals.org/ajcconline/article/34/2/95/32665/The-8-D-s-of-High-Flow-Nasal-Cannula-Risk-A

[^82]: http://arxiv.org/pdf/2408.04964.pdf

[^83]: https://arxiv.org/pdf/2404.18596.pdf

[^84]: https://www.aclweb.org/anthology/P16-4022.pdf

[^85]: https://joss.theoj.org/papers/10.21105/joss.02828.pdf

[^86]: https://academic.oup.com/nar/article-pdf/43/W1/W231/7476186/gkv400.pdf

[^87]: https://arxiv.org/html/2502.20077v2

[^88]: https://arxiv.org/html/2311.13035v2

[^89]: https://arxiv.org/pdf/2207.13591.pdf

[^90]: https://dev.to/sunmathi/-title-advanced-python-selenium-handling-iframes-actionchains-and-alerts--160b

[^91]: https://www.accelq.com/blog/selenium-with-python/

[^92]: https://scrapeops.io/selenium-web-scraping-playbook/python-selenium-make-selenium-undetectable/

[^93]: https://www.lambdatest.com/blog/top-python-frameworks-for-automation/

[^94]: https://www.pcloudy.com/blogs/utilising-selenium-python-for-advanced-web-automation/

[^95]: https://www.pcloudy.com/blogs/best-selenium-python-frameworks-for-test-automation/

[^96]: https://www.geeksforgeeks.org/python/selenium-python-tutorial/

[^97]: https://linguamatica.com/index.php/linguamatica/article/download/267/440

[^98]: https://periodicos.utfpr.edu.br/rbect/article/download/13014/pdf

[^99]: http://fics.edu.br/index.php/augusto_guzzo/article/download/224/323

[^100]: https://seer.ufrgs.br/index.php/renote/article/download/126654/85924

[^101]: http://www.scielo.br/pdf/edreal/v41n1/2175-6236-edreal-41-01-00091.pdf

[^102]: https://sol.sbc.org.br/livros/index.php/sbc/catalog/download/8/15/54-1

[^103]: https://www.devmedia.com.br/testes-automatizados-com-o-framework-selenium/32955

[^104]: https://www.homehost.com.br/blog/pythondjango/selenium-python/

[^105]: https://www.youtube.com/watch?v=myQIZElpXTU

[^106]: https://blog.geekhunter.com.br/automatizando-testes-com-python-selenium-e-behave/

[^107]: https://www.youtube.com/watch?v=x8VANjTyi-E

