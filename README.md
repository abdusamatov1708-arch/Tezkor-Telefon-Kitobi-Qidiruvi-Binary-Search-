# Tezkor-Telefon-Kitobi-Qidiruvi-Binary-Search-
// Telefon kitobi uchun ma'lumotlar bazasini yaratish va qidiruv algoritmlari

// Ma'lumotlar bazasini generatsiya qilish funksiyasi (saralangan holda)
function generatePhoneBook(n) {
    const phoneBook = [];
    for (let i = 1; i <= n; i++) {
        // Tartibli ismlar yaratamiz
        const paddedNum = String(i).padStart(5, '0');
        phoneBook.push({
            name: `Ism_${paddedNum}`,
            phone: `+99890${String(1000000 + i).slice(1)}`
        });
    }
    return phoneBook;
}

// 1-qism: Binary Search implementatsiyasi
function binarySearch(arr, targetName) {
    let left = 0;
    let right = arr.length - 1;
    let steps = 0;

    while (left <= right) {
        steps++;
        const mid = Math.floor((left + right) / 2);
        
        console.log(`[Binary Search] Qadam ${steps}: left=${left}, right=${right}, mid=${mid}`);

        if (arr[mid].name === targetName) {
            console.log(`-> Topildi! Indeks: ${mid}, Qadamlar soni: ${steps}`);
            return { index: mid, steps };
        } else if (arr[mid].name < targetName) {
            console.log(`-> Chap yarm kesib tashlandi (0 dan ${mid} gacha). O'ng tomonga o'tilmoqda.`);
            left = mid + 1;
        } else {
            console.log(`-> O'ng yarm kesib tashlandi (${mid} dan ${right} gacha). Chap tomonga o'tilmoqda.`);
            right = mid - 1;
        }
    }

    console.log(`-> Topilmadi. Jami qadamlar: ${steps}`);
    return { index: -1, steps };
}

// Linear Search implementatsiyasi
function linearSearch(arr, targetName) {
    let steps = 0;
    for (let i = 0; i < arr.length; i++) {
        steps++;
        if (arr[i].name === targetName) {
            return { index: i, steps };
        }
    }
    return { index: -1, steps };
}

// 2 va 3-qism: Telefon kitobi va Samaradorlik tahlili
const phoneBook1000 = generatePhoneBook(1000);
const target = "Ism_00750"; // Qidiriladigan element

console.log("--- BINARY SEARCH TESTI ---");
const bsResult = binarySearch(phoneBook1000, target);

console.log("\n--- LINEAR SEARCH TESTI ---");
const lsResult = linearSearch(phoneBook1000, target);
console.log(`Linear Search topdi: Indeks ${lsResult.index}, Qadamlar soni: ${lsResult.steps}`);

// O(log n) murakkablik izohi:
// Binary search har bir qadamda qidiruv maydonini 2 ga bo'ladi. 
// Shuning uchun 1000 ta element uchun maksimal qadamlar soni log2(1000) ≈ 10 ta qadamni tashkil etadi.
