# Automation Assignment-2

### registration form 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 20)

try:
    driver.get("https://www.amazon.in/")
    print("Amazon opened")

    search_box = wait.until(
        EC.element_to_be_clickable(
            (By.ID, "twotabsearchtextbox")
        )
    )

    search_box.send_keys("laptop")
    search_box.send_keys(Keys.ENTER)

    print("Search completed")

    wait.until(
        EC.presence_of_element_located(
            (By.CSS_SELECTOR, "div[data-component-type='s-search-result']")
        )
    )

    products = driver.find_elements(
        By.CSS_SELECTOR,
        "div[data-component-type='s-search-result']"
    )

    print("Products found:", len(products))

    for i, product in enumerate(products[:5], start=1):
        try:
            name = product.find_element(
                By.CSS_SELECTOR,
                "h2"
            ).text

            print(i, name)

        except:
            pass

    first_product = products[0]

    product_link = first_product.find_element(
        By.CSS_SELECTOR,
        "h2 a"
    )

    driver.execute_script(
        "arguments[0].click();",
        product_link
    )

    print("First product clicked")

    wait.until(
        EC.presence_of_element_located(
            (By.ID, "productTitle")
        )
    )

    print("Product page opened")
    add_to_cart = wait.until(
        EC.element_to_be_clickable(
            (By.ID, "add-to-cart-button")
        )
    )

    driver.execute_script(
        "arguments[0].click();",
        add_to_cart
    )

    print("Add to Cart clicked")

    time.sleep(3)

    cart_count = wait.until(
        EC.presence_of_element_located(
            (By.ID, "nav-cart-count")
        )
    )

    print("Cart count:", cart_count.text)

    if int(cart_count.text) > 0:
        print("ADD TO CART: PASS")
    else:
        print("ADD TO CART: FAIL")

    time.sleep(5)

except Exception as e:
    print("ERROR:", e)

finally:
    time.sleep(5)
    driver.quit()
```
## Output


<img width="1691" height="937" alt="Screenshot 2026-10-07 083654 - Copy" src="https://github.com/user-attachments/assets/e73111e7-4379-46d4-b149-323f26082699" />



<img width="1917" height="1078" alt="Screenshot 2026-10-07 083952" src="https://github.com/user-attachments/assets/4bb17c7b-6a88-4420-967e-6624a8e568d2" />



