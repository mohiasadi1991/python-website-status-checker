import tim
import urllib.request
import urllib.error

def check_website(url):
    if not url.startswith(("http://", "https://")):
        url = "https://" + url

    request = urllib.request.Request(
        url,
        headers={"User-Agent": "PythonStatusChecker"}
    )

    start = time.perf_counter()

    try:
        with urllib.request.urlopen(
            request, timeout=10
        ) as response:
            elapsed = time.perf_counter() - start

            print("\nWebsite:", url)
            print("Status:", response.status)
            print(f"Response time: {elapsed:.3f} seconds")
            print("Result: Website is online")

    except urllib.error.HTTPError as error:
        elapsed = time.perf_counter() - start
        print("\nWebsite:", url)
        print("Status:", error.code)
        print(f"Response time: {elapsed:.3f} seconds")
        print("Result: Website returned an HTTP error")

    except Exception as error:
        print("\nWebsite:", url)
        print("Result: Could not connect")
        print("Error:", error)

def main():
    print("=== Website Status Checker ===")
    print("Enter 'exit' to quit.\n")

    while True:
        url = input("Website URL: ").strip()

        if url.lower() == "exit":
            print("Goodbye!")
            break

        if not url:
            print("Please enter a valid URL.")
            continue

        check_website(url)

if __name__ == "__main__":
    main()
