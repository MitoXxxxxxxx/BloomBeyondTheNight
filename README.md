# BloomBeyondTheNight

# BBN
stars = []
flowers = []

meteorX = 0
meteorY = 0
meteorActive = False

def setup():
    size(1000, 700)

    for i in range(150):
        x = random(width)
        y = random(420)
        s = random(1, 4)

        brightness = random(150, 225)
        speed = random(0.2, 0.6)

        stars.append([x, y, s, brightness, speed])


def draw():
    global meteorX
    global meteorY
    global meteorActive

    # SKY CHANGES WITH FLOWERS
    flowerCount = len(flowers)

    daylight = map(flowerCount, 30, 50, 0, 1)
    daylight = constrain(daylight, 0, 1)

    skyR = 10 + 125 * daylight
    skyG = 15 + 191 * daylight
    skyB = 40 + 195 * daylight

    background(skyR, skyG, skyB)


    # STARS
    noStroke()

    for star in stars:
        x = star[0]
        y = star[1]
        s = star[2]
        brightness = star[3]

        fill(brightness)
        ellipse(x, y, s, s)

        star[3] = star[3] + star[4]

        if star[3] > 225:
            star[3] = 225
            star[4] = -star[4]

        if star[3] < 120:
            star[3] = 120
            star[4] = -star[4]


    # SHOOTING STAR
    if meteorActive:
        stroke(255)
        strokeWeight(4)

        line(meteorX, meteorY, meteorX - 60, meteorY - 35)

        noStroke()
        fill(255)

        ellipse(meteorX, meteorY, 10, 10)

        meteorX = meteorX + 8
        meteorY = meteorY + 5

        if meteorY > 500:
            flowerX = constrain(meteorX, 30, width - 30)

            r = random(180, 255)
            g = random(100, 220)
            b = random(150, 255)

            flowers.append([flowerX, 500, r, g, b])

            meteorActive = False


    # GRASS GRADIENT
    noStroke()

    for y in range(420, 500):
        value = map(y, 420, 500, 0, 1)

        r = skyR + (45 - skyR) * value
        g = skyG + (85 - skyG) * value
        b = skyB + (60 - skyB) * value

        fill(r, g, b)
        rect(0, y, width, 1)


    # MAIN GRASS
    fill(45, 85, 60)
    rect(0, 500, width, 200)


    # HOUSE

    # House body
    noStroke()
    fill(187, 152, 158)
    rect(80, 430, 180, 140)

    # Roof
    fill(82, 25, 19)
    triangle(60, 430, 280, 430, 170, 340)

    # Door
    fill(105, 82, 157)
    rect(150, 500, 40, 70)

    # Window
    fill(205, 173, 79)
    rect(105, 465, 35, 35)
    rect(200, 465, 35, 35)
  
    # TEXT
    fill(27, 72, 58)
    textSize(36)
    text("BLOOM BEYOND the NIGHT", 520, 620)

    # STONE PATH
    noStroke()

    fill(150, 150, 150)
    ellipse(250, 590, 24, 18)
    ellipse(285, 610, 20, 15)

    fill(170, 170, 170)
    ellipse(320, 630, 26, 18)
    ellipse(355, 650, 22, 16)

    fill(130, 130, 130)
    ellipse(390, 670, 24, 17)


    # FLOWERS
    for flower in flowers:
        x = flower[0]
        y = flower[1]

        r = flower[2]
        g = flower[3]
        b = flower[4]

        # Stem
        stroke(40, 110, 60)
        strokeWeight(3)
        line(x, y, x, y - 30)

        # Petals
        noStroke()
        fill(r, g, b)

        ellipse(x, y - 40, 14, 18)
        ellipse(x - 9, y - 33, 14, 18)
        ellipse(x + 9, y - 33, 14, 18)
        ellipse(x - 6, y - 22, 14, 18)
        ellipse(x + 6, y - 22, 14, 18)

        # Flower center
        fill(225, 210, 80)
        ellipse(x, y - 30, 10, 10)


# PRESS SPACE
def keyPressed():
    global meteorX
    global meteorY
    global meteorActive

    if key == ' ':
        meteorX = random(50, 500)
        meteorY = random(50, 250)

        meteorActive = True
        
       
