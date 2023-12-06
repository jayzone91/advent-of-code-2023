const fs = require("fs");
const path = require("path");

const regex = [
  /(?:\d)/g,
  /(?:one)/g,
  /(?:two)/g,
  /(?:three)/g,
  /(?:four)/g,
  /(?:five)/g,
  /(?:six)/g,
  /(?:seven)/g,
  /(?:eight)/g,
  /(?:nine)/g,
];

const table = [
  {
    name: "one",
    value: "1",
  },
  {
    name: "two",
    value: "2",
  },
  {
    name: "three",
    value: "3",
  },
  {
    name: "four",
    value: "4",
  },
  {
    name: "five",
    value: "5",
  },
  {
    name: "six",
    value: "6",
  },
  {
    name: "seven",
    value: "7",
  },
  {
    name: "eight",
    value: "8",
  },
  {
    name: "nine",
    value: "9",
  },
];

async function main() {
  const allNumbers = [];
  // TODO: Read File line by line
  const file = fs.readFileSync(path.join(__dirname, "input.txt"), "utf-8");
  file.split(/\r?\n/).forEach((line) => {
    if (line.length >= 1) {
      let indexes = {
        lowestIndex: null,
        highestIndex: null,
      };
      regex.forEach((reg) => {
        indexes = checkIndex(
          [...line.matchAll(reg)],
          indexes.lowestIndex,
          indexes.highestIndex
        );
      });
      let firstDigit = indexes.lowestIndex.match;
      if (firstDigit.length > 1) {
        const tmp = table.find((x) => x.name == firstDigit);
        firstDigit = tmp.value;
      }
      let lastDigit = indexes.highestIndex.match;
      if (lastDigit.length > 1) {
        const tmp = table.find((x) => x.name == lastDigit);
        lastDigit = tmp.value;
      }
      const newNumber = firstDigit + lastDigit;
      allNumbers.push(newNumber);
    }
  });
  const sum = addAll(allNumbers);
  console.log("Sum", sum);
}

void main();

function addAll(inp) {
  let s = 0;
  inp.forEach((x) => {
    s = s + parseInt(x);
  });
  return s;
}

function checkIndex(match, idxLow, idxHi) {
  if (match.length > 0) {
    let lowest = idxLow;
    let highest = idxHi;
    const low = match[0].index;
    const high = match[match.length - 1].index;
    if (low == null) return { lowestIndex: idxLow, highestIndex: idxHi };
    if (idxLow == null) {
      lowest = {
        match: match[0][0],
        idx: low,
      };
    } else if (idxLow.idx > low) {
      lowest = {
        match: match[0][0],
        idx: low,
      };
    }
    if (high == null) return { lowestIndex: idxLow, highestIndex: idxHi };
    if (idxHi == null) {
      highest = {
        match: match[match.length - 1][0],
        idx: high,
      };
    } else if (idxHi.idx < high) {
      highest = {
        match: match[match.length - 1][0],
        idx: high,
      };
    }
    return { lowestIndex: lowest, highestIndex: highest };
  } else {
    return { lowestIndex: idxLow, highestIndex: idxHi };
  }
}
