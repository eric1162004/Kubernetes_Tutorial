FROM golang:latest as builder
WORKDIR /app
COPY go.mod ./
RUN go mod download
COPY . .
RUN go build -o main .

FROM gcr.io/distroless/base-debian11
COPY --from=builder /app/main .
EXPOSE 80
ENTRYPOINT [ "./main" ]

