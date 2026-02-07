async / await
async function loadData() {
  try {
    const data = await fetchData()
    console.log(data)
  } catch (e) {
    console.error(e)
  }
}


👉 Dễ đọc hơn .then()