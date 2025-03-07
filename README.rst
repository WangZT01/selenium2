Selenium 2
============

Extends the python's selenium library by providing easy-to-use methods at the
cost of customizability. Provides site-specific methods such as login/logout
for quick browser automation.

Usage
------------

Instantiate a simple chrome browser

.. code-block:: python

    chrome = Browser('chrome')
    chrome.goto('github.com')

Instantiate a firefox browser to run through a proxy

.. code-block:: python

    firefox = Browser('firefox', ip='192.0.0.1:12345')

`NOTE: browser specific drivers need to be present and their path needs to be
appended in the system's PATH variable.`
DOWNLOAD LINK: https://www.seleniumhq.org/download/

Available Methods
-----------------

A base instance of ``Browser`` will have all the following methods. Note that you
can still access the underlying selenium driver for more fine grained control
through ``Browser.driver``.

.. code-block:: python

    def assert_proxy_is(self, ip:str) -> NoReturn: ...
    def set_implicit_wait(self, time_to_wait: int) -> NoReturn: ...
    def unset_implicit_wait(self) -> NoReturn: ...

    """ from browser.pu """
    def __init__(self, browser: str = 'ff' , desired_capabilities: dict = None,
            profile: object = None, options: object = None) -> NoReturn: ...
    # site-specific methods (must 'set_site_behaviour' first)
    def set_site_behaviour(self, Type[SiteBehaviour]) -> NoReturn: ...
    def create_account(self, details: dict, cookies: str = None) -> bool: ...
    def is_signed_in(self) -> bool: ...
    def is_signed_out(self) -> bool: ...
    def post(self, details: dict) -> str: ...
    def sign_in(self, details: dict, cookies: str = None) -> NoReturn: ...
    def sign_out(self) -> NoReturn: ...

    """ from base.py """
    def find_element(self, locator: U[WebElement, str], required: bool=True,
            parent: U[WebDriver, WebElement]=None) -> WebElement : ...
    def find_elements(self, locator: str, required: bool=False,
            parent: U[WebDriver, WebElement]=None) -> List[WebElement] : ...
    def is_text_present(self, text: str) -> bool: ...
    def is_element_enabled(self, locator: U[WebElement, str], tag: str=None) -> bool: ...
    def is_visible(self, locator: U[WebElement, str]) -> bool: ...

    """ from alert.py """
    def get_alert(self, timeout: int=DEFAULT_TIMEOUT, message: str ='') -> Alert: ...
    def get_alert_text(self, timeout: int=DEFAULT_TIMEOUT) -> str: ...
    def handle_alert(self, action: str='accept', timeout: int=DEFAULT_TIMEOUT) -> str: ...
    def input_text_into_alert(self, text: str, action: str='accept',
            timeout: int=None) -> str: ...

    """ from browsermanagement.py """
    def back(self) -> NoReturn: ...
    def forward(self) -> NoReturn: ...
    def get_session_id(self) -> str: ...
    def get_source(self) -> str: ...
    def get_title(self) -> str: ...
    def get_url(self) -> str: ...
    def goto(self, url: str) -> NoReturn: ...
    def refresh(self) -> NoReturn: ...
    def quit(self) -> NoReturn: ...

    """ from cookies.py """
    def add_cookie(self, cookie_dict: dict) -> NoReturn: ...
    def delete_all_cookies(self) -> NoReturn: ...
    def delete_cookie(self, name: str) -> NoReturn: ...
    def get_cookie(self, name:str) -> U[str, None]: ...
    def get_cookies(self) -> List[dict]: ...
    def load_cookies(self, filename: str, path: str='default') -> NoReturn: ...
    def save_cookies(self, filename: str) -> str: ...
    def set_cookies_directory(self, path: str=None, append: bool=True) -> str: ...
    def set_cookies_expiry(self, date: int=3735325880) -> NoReturn: ...

    """ from element.py """
    def clear_element_text(self, locator: U[WebElement, str]) -> NoReturn: ...
    def click_element(self, locator: U[WebElement, str]) -> NoReturn: ...
    def click_element_at_coordinates(self, locator: U[WebElement, str],
            xoffset: int, yoffset: int) -> NoReturn: ...
    def double_click_element(self, locator: U[WebElement, str]) -> NoReturn: ...
    def drag_and_drop(self, locator: U[WebElement, str],
            target: U[WebElement, str]) -> NoReturn: ...
    def element_text_contains(self, locator: U[WebElement, str], expected: str,
            ignore_case: bool=True) -> bool: ...
    def element_text_is(self, locator: U[WebElement, str], expected: str,
            ignore_case: bool=False) -> bool: ...
    def get_element_attribute(self, locator: U[WebElement, str], attribute: str) -> str: ...
    def get_element_property(self, locator: U[WebElement, str], prop: str) -> str: ...
    def get_element_size(self, locator: U[WebElement, str]) -> (int, int): ...
    def get_text(self, locator: U[WebElement, str]) -> str: ...
    def page_contains_text(self, text:str) -> bool: ...
    def right_click_element_at_coordinates(self, locator: U[WebElement, str],
            xoffset: int, yoffset: int) -> NoReturn: ...
    def send_keys(self, locator: U[WebElement, str]=None,
            *keys: U[List[str], str]) -> NoReturn: ...
    def highlight_elements(self, locator: U[List[WebElement], WebElement, str],
            tag: str=None) -> NoReturn: ...
    def set_focus_to_element(self, locator: U[WebElement, str]) -> NoReturn: ...
    def mouse_down(self, locator: U[WebElement, str]) -> NoReturn: ...
    def mouse_out(self, locator: U[WebElement, str]) -> NoReturn: ...
    def mouse_over(self, locator: U[WebElement, str]) -> NoReturn: ...
    def mouse_up(self, locator: U[WebElement, str]) -> NoReturn: ...
    def scroll_element_into_view(self, locator: U[WebElement, str]) -> NoReturn: ...
    def simulate_event(self, locator: U[WebElement, str], event: str) -> NoReturn: ...

    """ from frames.py """
    def send_method_to_element_in_frame(self, frame_locator: U[WebElement, str, int],
            element_locator: U[WebElement, str], method: Callable) -> Any: ...
    def switch_to_frame(self, locator: U[WebElement, str, int]) -> NoReturn: ...
    def unselect_frame(self) -> NoReturn: ...

    """ from javascript.py """
    def execute_javascript(self, script, *args: List[str]) -> Any: ...
    def execute_async_javascript(self, script, *args: List[str]) -> Any: ...

    """ from screenshot.py """
    def capture_element_screenshot(self, locator: U[WebElement, str],
            filename: str='element-screenshot-{index:03}.png') -> str: ...
    def capture_page_screenshot(self, filename: str='screenshot-{index:03}.png') -> str: ...
    def set_screenshot_directory(self, path: str=None, append: bool=True) -> str: ...

    """ from selects.py """
    def get_select_items(self, locator: U[WebElement, str], values:bool=False) -> List[str]: ...
    def get_selected_item(self, locator: U[WebElement, str], values: bool=False) -> str: ...
    def select_all_from_multilist(self, locator: U[WebElement, str]) -> NoReturn: ...
    def select_from_list_by_index(self, locator: U[WebElement, str],
            *indexes: str) -> NoReturn: ...
    def select_from_list_by_value(self, locator: U[WebElement, str],
            *values: str) -> NoReturn: ...
    def select_from_list_by_label(self, locator: U[WebElement, str],
            *labels: str) -> NoReturn: ...
    def unselect_all_from_list(self, locator: U[WebElement, str]) -> NoReturn: ...
    def unselect_from_list_by_index(self, locator: U[WebElement, str],
            *indexes: str) -> NoReturn: ...
    def unselect_from_list_by_value(self, locator: U[WebElement, str],
            *values: str) -> NoReturn: ...
    def unselect_from_list_by_label(self, locator: U[WebElement, str],
            *labels: str) -> NoReturn: ...

    """ from tables.py """
    def get_table_cell_by_index(self, locator: U[WebElement, str],
            row: U[str, int], column: U[str, int]) -> WebElement: ...
    def get_table_cell_text(self, locator: U[WebElement, str],
            row: U[str, int], column: U[str, int]) -> U[str, None]: ...
    def get_table_cell_by_text(self, locator: U[WebElement, str],
            text: str) -> str: ...
    def get_table_row_by_index(self, locator: U[WebElement, str],
            row: U[str, int]) -> List[WebElement]: ...
    def get_table_row_by_text(self, locator: U[WebElement, str],
            text: str) -> List[WebElement]: ...

    """ from waiting.py """
    def wait_for_element(self, locator: U[WebElement, str], negate:bool =False,
            timeout: int=DEFAULT_TIMEOUT,
            parent: U[WebDriver, WebElement]=None) -> WebElement: ...
    def wait_for_element_to_be_enabled(self, locator: U[WebElement, str],
            negate: bool=False, timeout: int=DEFAULT_TIMEOUT) -> WebElement : ...
    def wait_for_element_to_be_visible(self, locator, negate=False,
            timeout=DEFAULT_TIMEOUT) -> WebElement: ...
    def wait_for_element_to_contain(self, locator: U[WebElement, str],
            text: str, negate: bool=False,
            timeout: int=DEFAULT_TIMEOUT) -> WebElement: ...
    def wait_for_script(self, condition: str, negate: bool=False,
            timeout: int=DEFAULT_TIMEOUT, message: str='msg') -> Any: ...
    def wait_for_page_to_contain(self, text: str, negate:bool =False,
            timeout: int=DEFAULT_TIMEOUT)->bool: ...

    """ from windowmanager.py """
    def select_window(self, locator: U[List[str], str], timeout:int=None) -> str: ...
    def close_window(self) -> NoReturn: ...
    def get_all_windows_handles(self) -> List[str]: ...
    def get_all_windows_ids(self) -> List[str]: ...
    def get_all_windows_names(self) -> List[str]: ...
    def get_all_windows_titles(self) -> List[str]: ...
    def get_all_windows_urls(self) -> List[str]: ...
    def get_window_handle(self) -> str: ...
    def get_window_info(self) -> NamedTuple: ...
    def get_window_position(self) -> Tuple[int,int]: ...
    def get_window_size(self) -> Tuple[int,int]: ...
    def maximize_browser_window(self) -> NoReturn: ...
    def set_window_id(self, id: U[str, int]) -> NoReturn: ...
    def set_window_name(self, name: U[str, int]) -> NoReturn: ...
    def set_window_position(self, x: U[str, int], y: U[str, int]) -> NoReturn: ...
    def set_window_size(self, width: U[str, int],
            height: U[str, int]) -> NoReturn: ...


Site-specific methods
---------------------

Additional site-specific methods are available, but a site must be set first.
This ca be done using ``Browser.set_site_behaviour(SiteBehaviour)``

For instance, before you can use 'sign_in' or 'create_account', you must indicate
for which site you would like this behaviour to occur.

.. code-block:: python

    chrome = Browser('chrome')

    chrome.set_site_behaviour(Facebook)
    chrome.sign_in(credentials)
    chrome.post_content(details)
    chrome.sign_out()

    chrome.set_site_behaviour(X)
    chrome.sign_in(credentials)
    chrome.post_content(ad)
    chrome.sign_out()

The following are site-specific methods which require a site to be set first.

.. code-block:: python

    def create_account(self, details: dict, cookies: str = None): ...
    def create_content(self, details: dict) -> str: ...
    def delete_content(self, details: dict) -> bool: ...
    def edit_content(self, details: dict) -> bool: ...
    def is_signed_in(self) -> bool: ...
    def is_signed_out(self) -> bool: ...
    def sign_in(self, details: dict, cookies: str = None) -> NoReturn: ...
    def sign_out(self) -> NoReturn: ...

Environment Variables
---------------------

The following environment variables can be set to configure various aspects of the Selenium2 behavior:

``DEBUG``
    Controls the debug output of the Selenium2 wrapper. Set to ``True`` to enable verbose logging.
    Default is ``False``.

    .. code-block:: bash

        export SELENIUM2_DEBUG=True

``SELENIUM2_DEFAULT_TIMEOUT``
    Specifies the default timeout in seconds for explicit waits.
    Default is 15 seconds.

    .. code-block:: bash

        export SELENIUM2_DEFAULT_TIMEOUT=30

``SELENIUM2_SCREENSHOT_PATH``
    Sets the directory where screenshots will be saved.
    Default is 'screenshots'.

    .. code-block:: bash

        export SELENIUM2_SCREENSHOT_PATH='/path/to/screenshots'

``SELENIUM2_COOKIES_PATH``
    Defines the directory for storing browser cookies.
    Default is 'cookies'.

    .. code-block:: bash

        export SELENIUM2_COOKIES_PATH='/path/to/cookies'

These environment variables allow you to customize the behavior of the Selenium2 wrapper without changing the code. They are particularly useful for adapting the wrapper to different testing environments or requirements.

Contributing
------------

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

License
-------

Apache 2.0