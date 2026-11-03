const APPS_SCRIPT_URL =
"https://script.google.com/macros/s/AKfycbwFYk1OpuFrZ1KJZszsQ0QUgHTjl7G1wnbOCefw1vYgvGnX7A6rvbcae6Zra_e0iViy/exec";

exports.handler = async function () {
  try {
    const response = await fetch(
      APPS_SCRIPT_URL + "?t=" + Date.now(),
      {
        method: "GET",
        headers: {
          "Accept": "application/json"
        },
        redirect: "follow"
      }
    );

    const body = await response.text();

    if (!response.ok) {
      throw new Error("Apps Script HTTP " + response.status);
    }

    const payload = JSON.parse(body);

    if (!payload.ok || !Array.isArray(payload.devices)) {
      throw new Error("Invalid Google Sheets response");
    }

    return {
      statusCode: 200,
      headers: {
        "Content-Type": "application/json",
        "Cache-Control": "no-store"
      },
      body: JSON.stringify(payload)
    };

  } catch (error) {
    return {
      statusCode: 502,
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        ok: false,
        error: error.message
      })
    };
  }
};
