<script>
  import BackgroundScroller from '../lib/BackgroundScroller.svelte';

  const images = [
    '/Maternal-Mortality-Data-Storytelling/map1.png',
    '/Maternal-Mortality-Data-Storytelling/map2.png',
    '/Maternal-Mortality-Data-Storytelling/map3.png',
    '/Maternal-Mortality-Data-Storytelling/birth.jpeg',
    '/Maternal-Mortality-Data-Storytelling/income.png'
  ];

const texts = [
  [
    `The following maps are from the Health Resources & Services Administration (HRSA)’s <a href="https://data.hrsa.gov/maps/mchb" target="_blank" rel="noopener noreferrer">Maternal and Infant Health Mapping Tool</a>, showing the OB-GYN provider rate per 100,000 people.`,
    "Healthcare resources like OB-GYN providers are notably scarcer in the South and Midwest regions of the U.S."
  ],
  [
    "This map shows the percentage of women aged 15–44 by race—White women in blue, and Black women in yellow.",
    "Take note of where the brightest regions appear, and compare them to the next map."
  ],
  [
    "Here, we see the population density of uninsured women aged 15–44.",
    "While both the South and Midwest face a shortage of healthcare access, Black women are uniquely affected—facing both higher rates of uninsurance and lack of care, with far greater population densities than their white counterparts."
  ],
  [
    "Beyond these challenges, Black households face significantly higher risks and bear disproportionate impacts.",
    "The average cost of childbirth in the U.S. can range from $10,000 to $20,000—even with insurance—and doesn’t account for complications like C-sections or NICU stays. Black women are at a heightened risk for such complications. (Pictured is Sharon Irving, PhD, MPH, MS, CHES—a CDC epidemiologist and lieutenant commander who tragically passed just weeks after giving birth).",
    "Meanwhile, chosen and often expensive reproductive procedures—such as IVF, genetic testing, and comprehensive prenatal/postpartum care—are far more accessible to white women."
  ],
  [
    `These charts are from the Black Wealth Data Center’s <a href="https://blackwealthdata.org/" target="_blank" rel="noopener noreferrer">Racial Wealth Equity Database</a>.`,
    "A single episode of medical debt can completely erase the net worth of a typical Black household—whose median net worth is ~$45,000—compared to ~$285,000 for white households."
  ]
];

  // Align last two left, others right
  const alignments = ['right', 'right', 'right', 'left', 'left'];
</script>

<BackgroundScroller {images} {texts} {alignments} />
